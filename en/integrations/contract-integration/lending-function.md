# Lending Function

## Mint

***

Supplying asset to lending pool and enable user to interest earning from supplied liquidity.

```jsx
public fun mint<T>(
    version: &Version,
    market: &mut Market,
    coin: Coin<T>,
    clock: &Clock,
    ctx: &mut TxContext,
  ): Coin<MarketCoin<T>> { }
```

**Parameters**

| **Name** | **Type** | **Description**                                                                  |
| -------- | -------- | -------------------------------------------------------------------------------- |
| version  | Version  | The version control object, contract version must match with this                |
| market   | Market   | The Scallop market object, it contains base assets, and related protocol configs |
| coin     | Coin     | The base asset to be supplied to the market                                      |
| clock    | Clock    | The SUI system Clock object                                                      |

**Return Values**

| Name       | Type | Description                                                                        |
| ---------- | ---- | ---------------------------------------------------------------------------------- |
| MarketCoin | Coin | The yield bearing coin also an coin that proof user has supplied asset on Scallop. |

{% hint style="info" %}
Note: If the yield-bearing coin is transferred to another address, it means that you have moved your supplied asset to that address, and the current address can no longer withdraw the assets. Only the receiving address can withdraw the assets.
{% endhint %}

**Events**

* **MintEvent** is emited when the supply tx success

**Errors**

* **73729:** Currently market not active.
* **81922**: Asset supply already reach limit cap.

**Example**:

{% tabs %}
{% tab title="Move" %}
```rust
module protocol::foo {

  use sui::clock::{Self, Clock};
  use sui::tx_context::{Self ,TxContext};
  use sui::coin::{Self, Coin};

  use scallop_protocol::mint::mint;
  use scallop_protocol::Market as ScallopMarket;
  use scallop_protocol::Version as ScallopVersion;

  public fun doFoo<T>(
    scallop_version: &ScallopVersion,
    scallop_market: &mut ScallopMarket,
    coin: Coin<T>,
    clock: &Clock,
    ctx: &mut TxContext
  ): Coin<MarketCoin<T>> {
     scallop_protocol::mint::mint<T>(
	scallop_version,
	scallop_market,
	coin,
	clock,
	ctx,
      )
  }
}
```


{% endtab %}

{% tab title="Typescript" %}
```tsx
import { getFullnodeUrl, SuiClient, } from '@mysten/sui.js/client';
import { SUI_CLOCK_OBJECT_ID } from '@mysten/sui.js/utils';
import { Ed25519Keypair } from '@mysten/sui/keypairs/ed25519';

const keypair = new Ed25519Keypair();
const address = keypair.getPublicKey().toSuiAddress();

const rpcUrl = getFullnodeUrl('mainnet');
const client = new SuiClient({ url: rpcUrl });
 
const SCALLOP_MARKET_OBJECT = "0xa757975255146dc9686aa823b7838b507f315d704f428cbadad2f4ea061939d9";
const SCALLOP_VERSION_OBJECT = "0x07871c4b3c847a0f674510d4978d5cf6f960452795e8ff6f189fd2088a3f6ac7";

const txb = new TransactionBlock();
txb.setSender();
const [sui] = txb.splitCoins(txb.gas, [1e9]);

const sCoin = txb.moveCall({
  target: "0xa45b8ffca59e5b44ec7c04481a04cb620b0e07b2b183527bca4e5f32372c5f1a::mint::mint",
  arguments: [
    txb.object(SCALLOP_VERSION_OBJECT),
    txb.object(SCALLOP_MARKET_OBJECT),
    sui,
    txb.object(SUI_CLOCK_OBJECT_ID),
  ],
  typeArguments: ["0x2::sui::SUI"],
});

txb.transferObjects([sCoin], txb.pure(address));

await client.signAndExecuteTransaction({
  signer: getKeyPair(keypair),
  transaction: txb,
  requestType: 'WaitForLocalExecution',
  options: {
    showEffects: true,
  },
});
```


{% endtab %}
{% endtabs %}

## **Redeem**

***

Withdraw assets from Scallop on Lending Pools, but there’s one thing to remember here is you need your sCoin object to withdraw assets from pool.

```rust
public fun redeem<T>(
  version: &Version,
  market: &mut Market,
  coin: Coin<MarketCoin<T>>,
  clock: &Clock,
  ctx: &mut TxContext,
): Coin<T> { }
```

**Paremeters**:

| **Name** | **Type**          | **Description**                                                                  |
| -------- | ----------------- | -------------------------------------------------------------------------------- |
| version  | Version           | The version control object, contract version must match with this                |
| market   | Market            | The Scallop market object, it contains base assets, and related protocol configs |
| coin     | Coin\<MarketCoin> | The sCoin object to exchange for underlying base asset                           |
| clock    | Clock             | The SUI system Clock object                                                      |

**Return Value**:

| Name | Type | Description                   |
| ---- | ---- | ----------------------------- |
| Coin | Coin | The redeemed underlying asset |

**Events**

* **RedeemEvent** is emited when the withdraw tx success

**Errors**

* **2050:** The marketcoin used to redeem the assets is to small.
* **81924**: Reserve not enough.
* **81921**: Pool liquidity not enough to redeemed underlying assets.

**Example**:

{% tabs %}
{% tab title="Move" %}
```rust
module protocol::foo {

  use sui::tx_context::{Self ,TxContext};
  use sui::coin::{Self, Coin};
  use sui::coin::{Self, Coin};

  use scallop_protocol::mint::mint;
  use scallop_protocol::Market as ScallopMarket;
  use scallop_protocol::Version as ScallopVersion;

  public fun doFoo<T>(
    scallop_version: &ScallopVersion,
    scallop_market: &mut ScallopMarket,
    s_coin: Coin<MarketCoin<T>>,
    clock: &Clock,
    ctx: &mut TxContext
  ): Coin<MarketCoin<T>> {
     scallop_protocol::redeem::redeem<T>(
	scallop_version,
	scallop_market,
	s_coin,
	clock,
	ctx,
     )
  }
}
```
{% endtab %}

{% tab title="Typescript" %}
<pre class="language-tsx"><code class="lang-tsx">import { getFullnodeUrl, SuiClient, } from '@mysten/sui.js/client';
import { SUI_CLOCK_OBJECT_ID } from '@mysten/sui.js/utils';
import { Ed25519Keypair } from '@mysten/sui/keypairs/ed25519';

const keypair = new Ed25519Keypair();
const address = keypair.getPublicKey().toSuiAddress();

const rpcUrl = getFullnodeUrl('mainnet');
const client = new SuiClient({ url: rpcUrl });
 
const SCALLOP_MARKET_OBJECT = "0xa757975255146dc9686aa823b7838b507f315d704f428cbadad2f4ea061939d9";
const SCALLOP_VERSION_OBJECT = "0x07871c4b3c847a0f674510d4978d5cf6f960452795e8ff6f189fd2088a3f6ac7";

const getSCoin = await client.getCoins({
  owner: address,
 coinType: "0xefe8b36d5b2e43728cc323298626b83177803521d195cfb11e15b910e892fddf::reserve::MarketCoin&#x3C;0x0000000000000000000000000000000000000000000000000000000000000002::sui::SUI>"
});

const sCoinObjects = getScoin.map((scoin) => scoin.coinObjectId);
if(sCoinObjects.length > 0) {
  const txb = new TransactionBlock();
  txb.setSender();

  if(sCoinObjects.length > 1) {
    txb.merge(sCoinObjects[0], sCoinObjects.slice(1, sCoinObjects.length);
  }

  const [sSUI] = txb.splitCoins(sCoinObjects[0], [1e9]);
  const sCoin = txb.moveCall({
   target: "0xa45b8ffca59e5b44ec7c04481a04cb620b0e07b2b183527bca4e5f32372c5f1a::redeem::redeem",
   arguments: [
     txb.object(SCALLOP_VERSION_OBJECT),
     txb.object(SCALLOP_MARKET_OBJECT),
     sSUI,
     txb.object(SUI_CLOCK_OBJECT_ID),
   ],
   typeArguments: ["0xefe8b36d5b2e43728cc323298626b83177803521d195cfb11e15b910e892fddf::reserve::MarketCoin&#x3C;0x0000000000000000000000000000000000000000000000000000000000000002::sui::SUI>"],
<strong>  });
</strong>
  txb.transferObjects([sCoin], txb.pure(address));

  await client.signAndExecuteTransaction({
    signer: getKeyPair(keypair),
    transaction: txb,
    requestType: 'WaitForLocalExecution',
    options: {
	showEffects: true,
    },
 });
}
</code></pre>


{% endtab %}
{% endtabs %}
