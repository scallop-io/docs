# Borrowing Asset

After [depositing any collateral assets](deposit-withdraw-collateral.md), users can borrow any asset using their Obligation Account. Borrowed assets accrue interest, and must be repaid to unlock the collateral.

{% hint style="warning" %}
Borrowing is limited by the collateral's borrow capacity. If the obligation becomes unhealthy, it can be liquidated. Check the risk level with [Querying Obligation Accounts](../querying-obligation-accounts.md).
{% endhint %}

## Borrow Asset

#### Using ScallopClient

`borrow` requires the obligation id and the obligation key. Both can be read with `getObligations`.

{% hint style="info" %}
If the obligation is staked in the borrow incentive program, `ScallopClient.borrow` unstakes it before borrowing and stakes it again afterwards, in the same transaction.
{% endhint %}

```typescript
import { ScallopClient } from '@scallop-io/sui-scallop-sdk';

const scallopClient = new ScallopClient({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  secretKey: '...', // or mnemonics: '...'
});

await scallopClient.init();

const poolName = 'usdc';
const amount = 1e6; // 1 USDC

const obligations = await scallopClient.query.getObligations();
const { id: obligationId, keyId: obligationKey } = obligations[0];

const { effects, digest } = await scallopClient.borrow(
  poolName,
  amount,
  true, // sign and send the transaction
  obligationId,
  obligationKey
);
console.log(`${effects?.status.status}: ${digest}`);
```

#### Using ScallopBuilder

**Quick Method for Automatic Price Updates**

`borrowQuick` updates the X-Oracle prices internally, and returns the borrowed coin.

```typescript
import { ScallopBuilder } from '@scallop-io/sui-scallop-sdk';

const scallopBuilder = new ScallopBuilder({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  secretKey: '...', // or mnemonics: '...'
});

await scallopBuilder.init();

const poolName = 'usdc';
const amount = 1e6; // 1 USDC

const obligations = await scallopBuilder.query.getObligations();
const { id: obligationId, keyId: obligationKey } = obligations[0];

const tx = scallopBuilder.createTxBlock();
tx.setSender(scallopBuilder.walletAddress);

const borrowedCoin = await tx.borrowQuick(
  amount,
  poolName,
  obligationId,
  obligationKey
);
tx.transferObjects(
  [borrowedCoin],
  tx.pure.address(scallopBuilder.walletAddress)
);

const { effects, digest } = await scallopBuilder.signAndSendTxBlock(tx);
console.log(`${effects?.status.status}: ${digest}`);
```

**Normal Method for More Composability**

```typescript
import { ScallopBuilder } from '@scallop-io/sui-scallop-sdk';

const scallopBuilder = new ScallopBuilder({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  secretKey: '...', // or mnemonics: '...'
});

await scallopBuilder.init();

const poolName = 'usdc';
const amount = 1e6; // 1 USDC

const obligations = await scallopBuilder.query.getObligations();
const { id: obligationId, keyId: obligationKey } = obligations[0];

const tx = scallopBuilder.createTxBlock();
tx.setSender(scallopBuilder.walletAddress);

// Update prices of the obligation's collaterals, debts and the borrowed asset
const coinNames = await scallopBuilder.utils.getObligationCoinNames(obligationId);
await tx.updateAssetPricesQuick([...new Set([...coinNames, poolName])]);

const borrowedCoin = tx.borrow(
  tx.object(obligationId),
  tx.object(obligationKey),
  amount,
  poolName
);
tx.transferObjects(
  [borrowedCoin],
  tx.pure.address(scallopBuilder.walletAddress)
);

const { effects, digest } = await scallopBuilder.signAndSendTxBlock(tx);
console.log(`${effects?.status.status}: ${digest}`);
```

## Repay Asset

#### Using ScallopClient

```typescript
import { ScallopClient } from '@scallop-io/sui-scallop-sdk';

const scallopClient = new ScallopClient({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  secretKey: '...', // or mnemonics: '...'
});

await scallopClient.init();

const poolName = 'usdc';
const amount = 1e6; // 1 USDC

const obligations = await scallopClient.query.getObligations();
const { id: obligationId, keyId: obligationKey } = obligations[0];

const { effects, digest } = await scallopClient.repay(
  poolName,
  amount,
  true, // sign and send the transaction
  obligationId,
  obligationKey
);
console.log(`${effects?.status.status}: ${digest}`);
```

#### Using ScallopBuilder

**Quick Method for Automatic Coin Selection**

```typescript
import { ScallopBuilder } from '@scallop-io/sui-scallop-sdk';

const scallopBuilder = new ScallopBuilder({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  secretKey: '...', // or mnemonics: '...'
});

await scallopBuilder.init();

const poolName = 'usdc';
const amount = 1e6; // 1 USDC

const obligations = await scallopBuilder.query.getObligations();
const obligationId = obligations[0].id;

const tx = scallopBuilder.createTxBlock();
tx.setSender(scallopBuilder.walletAddress);

await tx.repayQuick(amount, poolName, obligationId);

const { effects, digest } = await scallopBuilder.signAndSendTxBlock(tx);
console.log(`${effects?.status.status}: ${digest}`);
```

**Normal Method for More Composability**

```typescript
import { ScallopBuilder } from '@scallop-io/sui-scallop-sdk';

const scallopBuilder = new ScallopBuilder({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  secretKey: '...', // or mnemonics: '...'
});

await scallopBuilder.init();

const poolName = 'usdc';
const amount = 1e6; // 1 USDC

const obligations = await scallopBuilder.query.getObligations();
const obligationId = obligations[0].id;

const tx = scallopBuilder.createTxBlock();
tx.setSender(scallopBuilder.walletAddress);

// Select the coin to repay with
const { takeCoin: repayCoin } = await scallopBuilder.selectCoin(
  tx,
  poolName,
  amount
);

tx.repay(tx.object(obligationId), repayCoin, poolName);

const { effects, digest } = await scallopBuilder.signAndSendTxBlock(tx);
console.log(`${effects?.status.status}: ${digest}`);
```
