# Flash Loan

A flash loan lets you borrow assets from a lending pool **without collateral**, as long as the loan plus the fee is returned within the **same transaction**. If the loan is not repaid, the whole transaction fails.

Common use cases are arbitrage, refinancing a position and self-liquidation.

## Check the Flash Loan Fee

The fee is returned as a decimal rate (e.g. `0.0005` is 0.05%). The amount you repay must cover the loan amount plus this fee.

```typescript
import { ScallopQuery } from '@scallop-io/sui-scallop-sdk';

const scallopQuery = new ScallopQuery({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  walletAddress: '0x...',
});

await scallopQuery.init();

const amount = 10 * 1e9; // 10 SUI
const fees = await scallopQuery.getFlashLoanFees(['sui']);
const fee = amount * fees.sui;
```

## Borrow and Repay a Flash Loan

#### Using ScallopClient

The callback receives the transaction block and the borrowed coin. It must return the coin that is used to repay, which must contain the loan amount plus the fee.

```typescript
import { ScallopClient } from '@scallop-io/sui-scallop-sdk';

const scallopClient = new ScallopClient({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  secretKey: '...', // or mnemonics: '...'
});

await scallopClient.init();

const poolName = 'sui';
const amount = 10 * 1e9; // 10 SUI

const { effects, digest } = await scallopClient.flashLoan(
  poolName,
  amount,
  (tx, coin) => {
    // Use the borrowed coin here, then return the coin to repay with
    return coin;
  }
);
console.log(`${effects?.status.status}: ${digest}`);
```

{% hint style="warning" %}
Returning the borrowed `coin` as is will fail, because it does not cover the fee. Merge a coin that covers the fee into it before returning.
{% endhint %}

#### Using ScallopBuilder

`borrowFlashLoan` returns the borrowed coin and a loan receipt. The receipt must be passed to `repayFlashLoan` in the same transaction.

```typescript
import { ScallopBuilder } from '@scallop-io/sui-scallop-sdk';

const scallopBuilder = new ScallopBuilder({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  secretKey: '...', // or mnemonics: '...'
});

await scallopBuilder.init();

const poolName = 'sui';
const amount = 10 * 1e9; // 10 SUI

const tx = scallopBuilder.createTxBlock();
tx.setSender(scallopBuilder.walletAddress);

const [loanCoin, loan] = tx.borrowFlashLoan(amount, poolName);

// Use the loanCoin here, e.g. swap, refinance, ...
// Then prepare a coin that covers the loan amount plus the fee
const repayCoin = loanCoin;

tx.repayFlashLoan(repayCoin, loan, poolName);

const { effects, digest } = await scallopBuilder.signAndSendTxBlock(tx);
console.log(`${effects?.status.status}: ${digest}`);
```
