# Claim Borrow Incentive Rewards

Borrowers earn incentive rewards while their Obligation Account is **staked** in the borrow incentive program. Rewards accrue per debt asset and are paid in the reward coin of the incentive pool (for example **SCA**).

## Stake/Unstake Obligation Account

An Obligation Account must be staked to earn rewards. Staking **locks** the obligation until it is unstaked.

#### Using ScallopClient

```typescript
import { ScallopClient } from '@scallop-io/sui-scallop-sdk';

const scallopClient = new ScallopClient({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  secretKey: '...', // or mnemonics: '...'
});

await scallopClient.init();

const obligations = await scallopClient.query.getObligations();
const { id: obligationId, keyId: obligationKey } = obligations[0];

// Stake
await scallopClient.stakeObligation(obligationId, obligationKey);

// Unstake
await scallopClient.unstakeObligation(obligationId, obligationKey);
```

#### Using ScallopBuilder

```typescript
import { ScallopBuilder } from '@scallop-io/sui-scallop-sdk';

const scallopBuilder = new ScallopBuilder({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  secretKey: '...', // or mnemonics: '...'
});

await scallopBuilder.init();

const obligations = await scallopBuilder.query.getObligations();
const { id: obligationId, keyId: obligationKey } = obligations[0];

const tx = scallopBuilder.createTxBlock();
tx.setSender(scallopBuilder.walletAddress);

// Obligation and key are optional, defaults to the user's first obligation
await tx.stakeObligationQuick(obligationId, obligationKey);
// await tx.unstakeObligationQuick(obligationId, obligationKey);

const { effects, digest } = await scallopBuilder.signAndSendTxBlock(tx);
console.log(`${effects?.status.status}: ${digest}`);
```

## Check Claimable Rewards

The claimable rewards are listed under each debt of the obligation account.

```typescript
import { ScallopQuery } from '@scallop-io/sui-scallop-sdk';

const scallopQuery = new ScallopQuery({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  walletAddress: '0x...',
});

await scallopQuery.init();

const account = await scallopQuery.getObligationAccount('0x...obligationId');

for (const [coinName, debt] of Object.entries(account?.debts ?? {})) {
  for (const reward of debt?.rewards ?? []) {
    console.log(
      `${coinName} debt: ${reward.availableClaimCoin} ${reward.coinName}`
    );
  }
}
```

## Claim Rewards

#### Using ScallopClient

```typescript
import { ScallopClient } from '@scallop-io/sui-scallop-sdk';

const scallopClient = new ScallopClient({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  secretKey: '...', // or mnemonics: '...'
});

await scallopClient.init();

const obligations = await scallopClient.query.getObligations();
const { id: obligationId, keyId: obligationKey } = obligations[0];

const { effects, digest } = await scallopClient.claimBorrowIncentive(
  obligationId,
  obligationKey
);
console.log(`${effects?.status.status}: ${digest}`);
```

#### Using ScallopBuilder

`claimBorrowIncentiveQuick` returns the reward coin of one reward type, so call it once for each reward coin.

```typescript
import { ScallopBuilder } from '@scallop-io/sui-scallop-sdk';

const scallopBuilder = new ScallopBuilder({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  secretKey: '...', // or mnemonics: '...'
});

await scallopBuilder.init();

const obligations = await scallopBuilder.query.getObligations();
const { id: obligationId, keyId: obligationKey } = obligations[0];

const tx = scallopBuilder.createTxBlock();
tx.setSender(scallopBuilder.walletAddress);

const rewardCoin = await tx.claimBorrowIncentiveQuick(
  'sca', // reward coin name
  obligationId,
  obligationKey
);
tx.transferObjects(
  [rewardCoin],
  tx.pure.address(scallopBuilder.walletAddress)
);

const { effects, digest } = await scallopBuilder.signAndSendTxBlock(tx);
console.log(`${effects?.status.status}: ${digest}`);
```
