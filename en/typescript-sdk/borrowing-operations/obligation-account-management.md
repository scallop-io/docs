# Obligation Account Management

## What is Obligation Account

An **Obligation Account** is a SUI shared object that represents a user’s borrowing position. It contains information about the user’s collateral deposits and borrowed assets.

An **Obligation Key** is generated and transferred to the user alongside the Obligation Account. This key serves as **proof of ownership** of the corresponding Obligation Account.

This design ensures **decentralization** and **security**, as only the holder of the Obligation Key has the authority to modify the associated Obligation Account.

{% hint style="warning" %}
**Warning!**\
Due to the decentralized design of the Obligation Key, **losing the key** will result in **permanent loss of access** to the associated Obligation Account.

Always **double-check your transactions** to ensure the **correct command** is used — for example, avoid transferring the Obligation Key to another user’s address or to a dead address.
{% endhint %}

## Creating An Obligation Account

Before users can deposit assets as collateral or borrow assets in Scallop, they must first create an Obligation Account.

The Scallop SDK provides several methods to create an Obligation Account, allowing developers to choose the approach that best fits their application flow.

#### Using ScallopClient

You can use the **`ScallopClient`** to create both the Obligation Account and the Obligation Key in a single operation.\
By default, the Obligation Key is automatically transferred to the sender’s wallet upon creation.

```typescript
import { ScallopClient } from '@scallop-io/sui-scallop-sdk';

const scallopClient = new ScallopClient({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  secretKey: '...', // or mnemonics: '...'
});

await scallopClient.init();

// Create obligation and obligation key, and transfer obligation key to sender
const { effects, digest } = await scallopClient.openObligation();
console.log(`${effects?.status.status}: ${digest}`);
```

#### Using ScallopBuilder

Using **`ScallopBuilder`** to create an Obligation Account and Obligation Key allows more flexibility.\
The Obligation Key can be used to perform **additional actions,** such as chaining operations **before** it is transferred to the sender’s wallet.

```typescript
import { ScallopBuilder } from '@scallop-io/sui-scallop-sdk';

const scallopBuilder = new ScallopBuilder({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  secretKey: '...', // or mnemonics: '...'
});

await scallopBuilder.init();

const tx = scallopBuilder.createTxBlock();
tx.setSender(scallopBuilder.walletAddress);

const [obligation, obligationKey, hotPotato] = tx.openObligation();

// Some operations with obligation and obligationKey
// e.g. deposit some assets into the obligation, borrow assets, 
// or stake the obligation account into incentive program

// Finally, return the obligation alongside the hot potato
tx.returnObligation(obligation, hotPotato);
// Transfer the obligation key to the user's address
tx.transferObjects(
  [obligationKey],
  tx.pure.address(scallopBuilder.walletAddress)
);
const { effects, digest } = await scallopBuilder.signAndSendTxBlock(tx);
console.log(`${effects?.status.status}: ${digest}`);
```
