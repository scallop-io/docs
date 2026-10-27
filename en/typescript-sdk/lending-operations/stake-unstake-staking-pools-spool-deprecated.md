# Stake/Unstake Staking Pools (spool) (deprecated)

## **Stake into spool**

There are several methods to stake sCoin into stake pool. Note that staking into spool will remove your existing sCoin from your wallet

#### Using ScallopClient

Using `ScallopClient` will automatically create a stake account if none exists.

```typescript
import { ScallopClient } from '@scallop-io/sui-scallop-sdk';

const scallopClient = new ScallopClient({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  secretKey: '...', // or mnemonics: '...'
});

await scallopClient.init();

const spoolName = 'ssca'; // Pool names are always in lowercases ('usdc', 'wal', 'sui', 'deep', 'sca', etc.)
const amount = 1 * 1e9; // 1 sSCA

const { effects, digest } = await scallopClient.stake(spoolName, amount);
console.log(`${effects?.status.status}: ${digest}`);
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

const spoolName = 'ssca'; // Pool names are always in lowercases ('usdc', 'wal', 'sui', 'deep', 'sca', etc.)
const amount = 1 * 1e9; // 1 sSCA

const tx = scallopBuilder.createTxBlock();
tx.setSender(scallopBuilder.walletAddress);

await tx.stakeQuick(amount, spoolName); // add `stakeAccountId` as third param for specific stake account

const { effects, digest } = await scallopBuilder.signAndSendTxBlock(tx);
console.log(`${effects?.status.status}: ${digest}`);
```

## **Unstake from spool**

#### Using ScallopClient

```typescript
import { ScallopClient } from '@scallop-io/sui-scallop-sdk';

const scallopClient = new ScallopClient({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  secretKey: '...', // or mnemonics: '...'
});

await scallopClient.init();

const spoolName = 'ssca'; // Pool names are always in lowercases ('usdc', 'wal', 'sui', 'deep', 'sca', etc.)
const amount = 1 * 1e9; // 1 sSCA

const { effects, digest } = await scallopClient.unstake(spoolName, amount);
console.log(`${effects?.status.status}: ${digest}`);
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

const spoolName = 'ssca'; // Pool names are always in lowercases ('usdc', 'wal', 'sui', 'deep', 'sca', etc.)
const amount = 1 * 1e9; // 1 sSCA

const tx = scallopBuilder.createTxBlock();
tx.setSender(scallopBuilder.walletAddress);

await tx.unstakeQuick(amount, spoolName); // add `stakeAccountId` as third param for specific stake account

const { effects, digest } = await scallopBuilder.signAndSendTxBlock(tx);
console.log(`${effects?.status.status}: ${digest}`);
```
