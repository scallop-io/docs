# Intro

## Scallop Typescript SDK

***

The Scallop SDK is a TypeScript library that provides a comprehensive interface for interacting with the Scallop lending protocol on the Sui blockchain. This document covers the SDK's architecture, core components, and integration patterns that enable developers to build applications leveraging Scallop's decentralized finance capabilities.

### Installation

```bash
npm install @scallop-io/sui-scallop-sdk
```

The SDK requires **Node.js 22 or newer** and is published as ESM and CJS.

### Core Classes

The Scallop SDK comprises several core classes, each with distinct responsibilities:

* **Scallop**\
  The **`Scallop`** class is the main class that can be used to initialize other classes.
* **ScallopClient**\
  The **`ScallopClient`** class serves as the main interface for interacting with the Scallop lending protocol on Sui. It offers a user-friendly, high-level API that simplifies transaction creation and protocol operations with accessible methods. ScallopClient encapsulates the functionality of the ScallopBuilder and provides convenient methods for DeFi operations such as lending, borrowing, staking, and collateral management. It is ideal for executing single operations.
* **ScallopBuilder**\
  The **`ScallopBuilder`** class is the core component of the Scallop SDK, designed to construct complex transactions within the Scallop DeFi protocol on Sui. It provides both low-level transaction building methods and high-level quick methods that manage coin selection and account management automatically. It is suitable for executing multiple operations.
* **ScallopQuery**\
  The **`ScallopQuery`** class is the main data retrieval tool of the Scallop SDK, providing access to on-chain data from the Scallop DeFi protocol. It offers market data, user portfolio details, staking information, and other protocol states via direct blockchain queries and optimized indexer services.
* **ScallopUtils**\
  The **`ScallopUtils`** class is the main class responsible for helper functions including parsing coin name and coin type, fetching coin prices, etc.

### Class Dependencies

The classes form a chain, where each class holds a reference to the next one:

* **`Scallop`** depends on `ScallopClient`.
* **`ScallopClient`** depends on `ScallopBuilder`.
* **`ScallopBuilder`** depends on `ScallopQuery`.
* **`ScallopQuery`** depends on `ScallopUtils`.

Each class exposes the next one as a property, e.g. `scallopClient.builder`, `scallopBuilder.query` and `scallopQuery.utils`.

### Initialization

Each class can be initialized independently. The `ScallopQuery` class can be initialized separately and then passed to the `ScallopBuilder`, and similarly for the `ScallopClient`. By default, initializing a `ScallopBuilder` automatically creates its own `ScallopQuery`. You have the flexibility to initialize these classes in any sequence you prefer.

#### Required Parameters

To send transactions (`Scallop`, `ScallopClient`, `ScallopBuilder`), the minimum parameters are:

* `addressId`: the Scallop address id, e.g. `'695fcdc084f790c04eb068dc'`
* `fullnodeUrl`: a Sui fullnode URL (or pass `suiClient` instead)
* `secretKey` **or** `mnemonics`: the signer

To only read data (`ScallopQuery`), replace the signer with `walletAddress`. A `walletAddress` alone cannot execute transactions.

#### All Parameters

```typescript
type CommonParams = {
  addressId: string; // Required
  fullnodeUrl?: string; // Required unless `suiClient` is given
  suiClient?: SuiGrpcClient; // Alternative to `fullnodeUrl`
  network?: 'mainnet' | 'testnet' | 'devnet';

  // Signer, choose one
  secretKey?: string;
  mnemonics?: string;
  walletAddress?: string; // read-only

  pythEndpoint?: string; // Pyth (Hermes) price service endpoint
  pythApiKey?: string;
  tokensPerSecond?: number; // Rate limit for on-chain reads
  priceTimeout?: number; // Pyth price cache lifetime in ms, defaults to 5000
  strictInit?: boolean; // Throw on init if required addresses/whitelist are missing
  logger?: Logger; // Defaults to a silent logger
};
```

#### Using Scallop class

```typescript
import { Scallop } from '@scallop-io/sui-scallop-sdk';

const scallop = new Scallop({
  addressId: '695fcdc084f790c04eb068dc',
  network: 'mainnet',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  secretKey: process.env.SECRET_KEY,
});

// using ScallopClient
const scallopClient = await scallop.createScallopClient();
// You can access ScallopBuilder and ScallopQuery directly from ScallopClient
const { builder, query } = scallopClient;

// Or initialize independently
const scallopQuery = await scallop.createScallopQuery();
```

#### Without using Scallop class

```typescript
import { ScallopQuery } from '@scallop-io/sui-scallop-sdk';

const scallopQuery = new ScallopQuery({
  addressId: '695fcdc084f790c04eb068dc',
  network: 'mainnet',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  walletAddress: '0x...',
});
await scallopQuery.init();
```

{% hint style="info" %}
After manual construction, always call `.init()`. The `create*` methods of the `Scallop` class call it for you.
{% endhint %}

### Read Transport (gRPC or GraphQL)

By default, reads use **gRPC** through `fullnodeUrl`. You can read through **GraphQL** instead by setting `readTransport: 'graphql'`. Transactions are always sent over gRPC, regardless of the read transport.

```typescript
const scallop = new Scallop({
  addressId: '695fcdc084f790c04eb068dc',
  network: 'mainnet',
  readTransport: 'graphql',
  graphqlUrl: 'https://graphql.mainnet.sui.io/graphql', // optional, defaults to mainnet
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443', // optional, used to send transactions
  walletAddress: '0x...',
});
```

### Smaller Imports

To keep your bundle small, import only the class you need from a subpath:

| Import path                           | Contains                                                     |
| ------------------------------------- | ------------------------------------------------------------ |
| `@scallop-io/sui-scallop-sdk`         | Everything                                                   |
| `@scallop-io/sui-scallop-sdk/client`  | `ScallopClient`                                              |
| `@scallop-io/sui-scallop-sdk/query`   | `ScallopQuery`                                               |
| `@scallop-io/sui-scallop-sdk/builder` | `ScallopBuilder`                                             |
| `@scallop-io/sui-scallop-sdk/errors`  | Typed error classes (`ScallopError`, `ScallopRpcError`, ...) |
| `@scallop-io/sui-scallop-sdk/logger`  | `consoleLogger`, `noopLogger`                                |
| `@scallop-io/sui-scallop-sdk/types`   | Types only                                                   |

### Logging and Errors

The SDK never prints to the console by default. To see its logs, pass a logger:

```typescript
import { consoleLogger } from '@scallop-io/sui-scallop-sdk/logger';

const scallopQuery = new ScallopQuery({ /* ... */ logger: consoleLogger });
```

Errors thrown by the SDK extend `ScallopError`, so you can check the type of the error instead of matching its message.
