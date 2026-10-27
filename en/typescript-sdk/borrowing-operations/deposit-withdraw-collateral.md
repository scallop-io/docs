# Deposit/Withdraw Collateral

Before users can borrow any assets, they must first deposit assets as collateral into their Obligation Account.

{% hint style="info" %}
`ScallopClient.depositCollateral` creates an Obligation Account automatically if the user has none. The `ScallopBuilder` quick methods do **not**; they throw an error if no obligation is found. See [Obligation Account Management](obligation-account-management.md) to create one manually.
{% endhint %}

## Deposit Collateral

#### Using ScallopClient

```typescript
import { ScallopClient } from '@scallop-io/sui-scallop-sdk';

const scallopClient = new ScallopClient({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  secretKey: '...', // or mnemonics: '...'
});

await scallopClient.init();

const coinName = 'sca';
const amount = 1e9; // 1 SCA

const { effects, digest } = await scallopClient.depositCollateral(
  coinName,
  amount
);
console.log(`${effects?.status.status}: ${digest}`);
```

To deposit into a specific obligation, pass the obligation id as the fourth argument: `depositCollateral(coinName, amount, true, obligationId)`.

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

const coinName = 'sca';
const amount = 1e9; // 1 SCA

// Get owned obligations
const obligations = await scallopBuilder.query.getObligations();
const obligationId = obligations[0].id;

const tx = scallopBuilder.createTxBlock();
tx.setSender(scallopBuilder.walletAddress);

await tx.depositCollateralQuick(amount, coinName, obligationId);

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

const coinName = 'sca';
const amount = 1e9; // 1 SCA

// Get owned obligations
const obligations = await scallopBuilder.query.getObligations();
const obligationId = obligations[0].id;

const tx = scallopBuilder.createTxBlock();
tx.setSender(scallopBuilder.walletAddress);

// Select collateral coin
const { takeCoin: collateralCoin } = await scallopBuilder.selectCoin(
  tx,
  coinName,
  amount
);

tx.depositCollateral(tx.object(obligationId), collateralCoin, coinName);

const { effects, digest } = await scallopBuilder.signAndSendTxBlock(tx);
console.log(`${effects?.status.status}: ${digest}`);
```

## Withdraw Collateral

Withdrawing collateral requires the latest asset prices, so that the protocol can verify the obligation stays healthy.

#### Using ScallopClient

```typescript
import { ScallopClient } from '@scallop-io/sui-scallop-sdk';

const scallopClient = new ScallopClient({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  secretKey: '...', // or mnemonics: '...'
});

await scallopClient.init();

const coinName = 'sca';
const amount = 1e9; // 1 SCA

const { effects, digest } = await scallopClient.withdrawCollateral(
  coinName,
  amount
);
console.log(`${effects?.status.status}: ${digest}`);
```

#### Using ScallopBuilder

**Quick Method for Automatic Price Updates**

```typescript
import { ScallopBuilder } from '@scallop-io/sui-scallop-sdk';

const scallopBuilder = new ScallopBuilder({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  secretKey: '...', // or mnemonics: '...'
});

await scallopBuilder.init();

const coinName = 'sca';
const amount = 1e9; // 1 SCA

// Get owned obligations
const obligations = await scallopBuilder.query.getObligations();
const obligationId = obligations[0].id;

const tx = scallopBuilder.createTxBlock();
tx.setSender(scallopBuilder.walletAddress);

// Returns the withdrawn collateral coin
const collateralCoin = await tx.takeCollateralQuick(
  amount,
  coinName,
  obligationId
);
tx.transferObjects(
  [collateralCoin],
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

const coinName = 'sca';
const amount = 1e9; // 1 SCA

// Get owned obligations
const obligations = await scallopBuilder.query.getObligations();
const { id: obligationId, keyId: obligationKey } = obligations[0];

const tx = scallopBuilder.createTxBlock();
tx.setSender(scallopBuilder.walletAddress);

// Update asset prices before taking collateral
await tx.updateAssetPricesQuick(
  await scallopBuilder.utils.getObligationCoinNames(obligationId)
);

const collateralCoin = tx.takeCollateral(
  tx.object(obligationId),
  tx.object(obligationKey),
  amount,
  coinName
);
tx.transferObjects(
  [collateralCoin],
  tx.pure.address(scallopBuilder.walletAddress)
);

const { effects, digest } = await scallopBuilder.signAndSendTxBlock(tx);
console.log(`${effects?.status.status}: ${digest}`);
```
