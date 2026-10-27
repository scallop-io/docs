# Querying Obligation Accounts

Use **`ScallopQuery`** to read the Obligation Accounts owned by a wallet, including their collaterals, debts and risk level. All methods below are read-only and do not require a `secretKey`; a `walletAddress` is enough.

```typescript
import { ScallopQuery } from '@scallop-io/sui-scallop-sdk';

const scallopQuery = new ScallopQuery({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  walletAddress: '0x...',
});

await scallopQuery.init();
```

## Get Owned Obligations

Returns the id, key id and lock status of every Obligation Account owned by the address. `locked` is `true` when the obligation is staked in the borrow incentive program.

```typescript
const obligations = await scallopQuery.getObligations();
// [{ id: '0x...', keyId: '0x...', locked: false }, ...]

// Query another wallet
const others = await scallopQuery.getObligations('0x...');
```

## Get Obligation Accounts Information

`getObligationAccounts` returns the detailed collateral and borrowing information of **all** obligations owned by the address, keyed by obligation id.

```typescript
const obligationAccounts = await scallopQuery.getObligationAccounts();

for (const account of Object.values(obligationAccounts)) {
  console.log(account?.obligationId);
  console.log(account?.totalDepositedValue); // total collateral value in USD
  console.log(account?.totalBorrowedValue); // total debt value in USD
  console.log(account?.totalRiskLevel); // above 1 means the obligation can be liquidated
}
```

To read a single obligation, use `getObligationAccount`:

```typescript
const account = await scallopQuery.getObligationAccount('0x...obligationId');

// Collaterals, keyed by coin name
const sca = account?.collaterals.sca;
console.log(sca?.depositedCoin); // deposited amount in coin unit
console.log(sca?.availableWithdrawCoin); // amount that can still be withdrawn

// Debts, keyed by coin name
const usdc = account?.debts.usdc;
console.log(usdc?.borrowedCoin); // borrowed amount in coin unit
console.log(usdc?.availableBorrowCoin); // amount that can still be borrowed
console.log(usdc?.availableRepayCoin); // amount that can be repaid
```

{% hint style="info" %}
Fields ending with `Amount` are in the coin's smallest unit (e.g. `1e9` for 1 SUI), while fields ending with `Coin` are in the coin's normal unit.
{% endhint %}

### Main Fields of `ObligationAccount`

| Field                           | Description                                                            |
| ------------------------------- | ---------------------------------------------------------------------- |
| `obligationId`                  | Obligation Account id                                                  |
| `totalDepositedValue`           | Total value of all deposited collaterals (USD)                         |
| `totalBorrowedValue`            | Total value of all debts (USD)                                         |
| `totalBorrowCapacityValue`      | Maximum debt value allowed by the collaterals (USD)                    |
| `totalAvailableCollateralValue` | Collateral value that is not required by the current debts (USD)       |
| `totalRiskLevel`                | Ratio of weighted debt to unhealthy collateral. Liquidatable above `1` |
| `collaterals`                   | Collateral details, keyed by coin name                                 |
| `debts`                         | Debt details (including borrow incentive rewards), keyed by coin name  |

## Query Raw Obligation Data

`queryObligation` returns the raw collateral and debt amounts of one obligation, without prices or risk calculation.

```typescript
const obligation = await scallopQuery.queryObligation('0x...obligationId');
console.log(obligation?.collaterals, obligation?.debts);
```

## Check If an Obligation is Locked

An obligation that is staked in the borrow incentive program is locked, and some actions (such as withdrawing collateral) are not available until it is unstaked.

```typescript
const locked = await scallopQuery.getObligationLocked('0x...obligationId');
```
