# Supply/Withdraw Asset

When users supply assets into Scallop lending pools, they receive [**sCoins**](../../scallop-lend/lending/scoin.md) — tokens that represent their **lending positions**. For example, depositing **SUI** yields **sSUI**, and depositing **USDC** yields **sUSDC**.

sCoins accrue value over time based on lending yields and can be **redeemed** to withdraw the underlying assets.

## Supply Asset

There are several methods to supply assets into lending pools. Users will receive sCoin as proof of their lending positions.

#### Using ScallopClient

```typescript
import { ScallopClient } from '@scallop-io/sui-scallop-sdk';

const scallopClient = new ScallopClient({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  secretKey: '...', // or mnemonics: '...'
});

await scallopClient.init();

const poolName = 'sca'; // Use lowercase for pool names ('usdc', 'wal', 'sui', 'deep', etc.)
const amount = 1 * 1e9; // 1 SCA

const { effects, digest } = await scallopClient.supply(poolName, amount);
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

const poolName = 'sca'; // Use lowercase for pool names
const amount = 1 * 1e9; // 1 SCA

const tx = scallopBuilder.createTxBlock();
tx.setSender(scallopBuilder.walletAddress);

// Quick supply with automatic coin selection, returns the sCoin
const sCoin = await tx.supplyQuick(amount, poolName);
tx.transferObjects([sCoin], tx.pure.address(scallopBuilder.walletAddress));

const { effects, digest } = await scallopBuilder.signAndSendTxBlock(tx);
console.log(`${effects?.status.status}: ${digest}`);
```

{% hint style="info" %}
`supplyQuick` returns an **sCoin** by default. Pass `false` as the third argument (`returnSCoin`) to receive the legacy **market coin** instead.
{% endhint %}

**Normal Method for More Composability**

```typescript
import { ScallopBuilder } from '@scallop-io/sui-scallop-sdk';

const scallopBuilder = new ScallopBuilder({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  secretKey: '...', // or mnemonics: '...'
});

await scallopBuilder.init();

const poolName = 'sca'; // Use lowercase for pool names
const amount = 1 * 1e9; // 1 SCA

const tx = scallopBuilder.createTxBlock(); // You can pass another tx into the `createTxBlock`
tx.setSender(scallopBuilder.walletAddress);

// Select the coin to supply
const { takeCoin } = await scallopBuilder.selectCoin(tx, poolName, amount);

// Supply returns a market coin, mint it into an sCoin
const marketCoin = tx.supply(takeCoin, poolName);
const sCoin = tx.mintSCoin(scallopBuilder.utils.parseMarketCoinName(poolName), marketCoin);

tx.transferObjects([sCoin], tx.pure.address(scallopBuilder.walletAddress));

const { effects, digest } = await scallopBuilder.signAndSendTxBlock(tx);
console.log(`${effects?.status.status}: ${digest}`);
```

## Withdraw Asset

There are several methods to withdraw supplied assets from lending pools. Note that withdrawal will burn user's existing sCoins.

#### Using ScallopClient

```typescript
import { ScallopClient } from '@scallop-io/sui-scallop-sdk';

const scallopClient = new ScallopClient({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  secretKey: '...', // or mnemonics: '...'
});

await scallopClient.init();

const poolName = 'sca'; // Use lowercase for pool names ('usdc', 'wal', 'sui', 'deep', etc.)
const amount = 1 * 1e9; // 1 SCA

const { effects, digest } = await scallopClient.withdraw(poolName, amount);
console.log(`${effects?.status.status}: ${digest}`);
```

#### Using ScallopBuilder

**Quick Method for Automatic Coin Selection**

`withdrawQuick` uses the user's sCoins first, and falls back to the old market coins when the sCoins are not enough.

```typescript
import { ScallopBuilder } from '@scallop-io/sui-scallop-sdk';

const scallopBuilder = new ScallopBuilder({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  secretKey: '...', // or mnemonics: '...'
});

await scallopBuilder.init();

const poolName = 'sca'; // Use lowercase for pool names
const amount = 1 * 1e9; // 1 SCA

const tx = scallopBuilder.createTxBlock();
tx.setSender(scallopBuilder.walletAddress);

const withdrawCoin = await tx.withdrawQuick(amount, poolName);
tx.transferObjects(
  [withdrawCoin],
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

const poolName = 'sca'; // Pool names are always in lowercases ('usdc', 'wal', 'sui', 'deep', etc.)
const amount = 1 * 1e9; // 1 SCA

const tx = scallopBuilder.createTxBlock();
tx.setSender(scallopBuilder.walletAddress);

const sCoinName = scallopBuilder.utils.parseSCoinName(poolName);
if (!sCoinName) throw new Error('Invalid pool name');

// Prioritize sCoins, then fall back to the old market coins
const { sCoin, marketCoin: oldMarketCoin } =
  await scallopBuilder.selectSCoinOrMarketCoin(tx, sCoinName, amount);

// Withdraw requires a market coin, burn the sCoin into a market coin first
let marketCoin = oldMarketCoin;
if (sCoin) {
  const burned = tx.burnSCoin(sCoinName, sCoin);
  if (marketCoin) {
    tx.mergeCoins(marketCoin, [burned]);
  } else {
    marketCoin = burned;
  }
}

if (!marketCoin) throw new Error(`No sCoin or market coin for ${poolName}`);
const coin = tx.withdraw(marketCoin, poolName);
tx.transferObjects([coin], tx.pure.address(scallopBuilder.walletAddress));

const { effects, digest } = await scallopBuilder.signAndSendTxBlock(tx);
console.log(`${effects?.status.status}: ${digest}`);
```
