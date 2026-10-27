# Updating X-Oracle Asset Prices

## What is X-Oracle

X-Oracle is an additional security layer developed by Scallop to **mitigate the risk of price manipulation in lending protocols** by using multiple oracles to cross-verify asset prices. A primary oracle provides the main data source, while additional oracles act as an additional data to verify the primary oracle’s accuracy. X-Oracle is utilized upon depositing collateral assets, borrowing assets, or [liquidating assets from unhealthy obligation](../../scallop-lend/liquidations.md).

## Updating Asset Prices

To update X-Oracle prices, you must first update the **underlying source oracle prices**. The SDK supports **Pyth**, **Supra** and **Switchboard** as source oracles, and picks the right one for each asset automatically based on the protocol configuration.

The quick methods in **`ScallopBuilder`** that need a price update already include the update call **internally**: `borrowQuick`, `takeCollateralQuick`, `borrowWithReferralQuick` and `liquidateQuick`. This means you **do not need to manually call** the X-Oracle update before executing these methods.

You can use **`updateAssetPricesQuick`** from **`ScallopTxBlock`** when you build your own flow with the normal methods. It automatically updates the underlying source oracle prices, ensuring that all price data used in subsequent calls of the same transaction is up to date.

```typescript
import { ScallopBuilder } from '@scallop-io/sui-scallop-sdk';

const scallopBuilder = new ScallopBuilder({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  secretKey: '...', // or mnemonics: '...'
});

await scallopBuilder.init();
const coinNames = ['sui', 'usdc', 'sca'];

const tx = scallopBuilder.createTxBlock();
tx.setSender(scallopBuilder.walletAddress);

// Update assets XOracle prices
await tx.updateAssetPricesQuick(coinNames);

// Some actions to be performed after updating prices
// ....

const { effects, digest } = await scallopBuilder.signAndSendTxBlock(tx);
console.log(`${effects?.status.status}: ${digest}`);
```

{% hint style="info" %}
`updateAssetPricesQuick` is asynchronous, always `await` it. If you omit the coin names, the prices of all assets are updated.
{% endhint %}
