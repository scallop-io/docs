# Liquidation Function

## L**iquidate**

***

This function allows you to liquidate an obligation account that has unhealthy condition. Anyone can perform the liquidation if the obligation is in unhealthy condition. Additionally, you need to update the oracle price before proceeding with the liquidation.

```rust
public fun liquidate<DebtType, CollateralType>(
  version: &Version,
  obligation: &mut Obligation,
  market: &mut Market,
  available_repay_coin: Coin<DebtType>,
  coin_decimals_registry: &CoinDecimalsRegistry,
  x_oracle: &XOracle,
  clock: &Clock,
  ctx: &mut TxContext,
): (Coin<DebtType>, Coin<CollateralType>) { }
```

**Modules**:

**Parameters**

| **Name**                 | **Type**             | **Description**                                                                  |
| ------------------------ | -------------------- | -------------------------------------------------------------------------------- |
| version                  | Version              | The version control object, contract version must match with this                |
| obligation               | Obligation           | The obligation id object                                                         |
| market                   | Market               | The Scallop market object, it contains base assets, and related protocol configs |
| available\_repay\_coin   | Coin                 | Coin object that used to repay the debt of obligation.                           |
| coin\_decimals\_registry | CoinDecimalsRegistry | The package that has decimal coin of base assets.                                |
| x\_oracle                | XOracle              | The x-oracle object which provides the price of assets                           |
| clock                    | Clock                | The SUI system clock object                                                      |

**Return Values**

| Name | Type | Description               |
| ---- | ---- | ------------------------- |
| Coin | Coin | The remaining base asset  |
| Coin | Coin | The liquidated collateral |

**Events**

* LiquidateEventV2 is emited when the supply tx success

**Errors**

* **770:** Means current obligation is locked and need to unstake first from borrow incentive
* **1537:** Unable liquidated because liquid amount is not lower than or equal 0

**Example**:

{% tabs %}
{% tab title="Move" %}
```rust
module protocol::foo {

  use sui::coin::{Self, Coin};

  use scallop_protocol::mint::mint;
  use scallop_protocol::Market as ScallopMarket;
  use scallop_protocol::Version as ScallopVersion;
  use scallop_protocol::Obligation;
  use scallop_protocol::CoinDecimalsRegistry;
  use scallop_protocol::XOracle;

  public fun doFoo<T>(
    scallop_version: &Version,
    obligation: &mut Obligation,
    scallop_market: &mut Market,
    available_repay_coin: Coin<DebtType>,
    coin_decimals_registry: &CoinDecimalsRegistry,
    x_oracle: &XOracle,
    clock: &Clock,
    ctx: &mut TxContext
  ): Coin<MarketCoin<T>> {
    scallop_protocol::liquidate::liquidate<T>(
      scallop_version,
      scallop_market,
      available_repay_coin,
      coin_decimals_registry,
      x_oracle,
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
const SCALLOP_COIN_DECIMAL_REGISTRY = "0x200abe9bf19751cc566ae35aa58e2b7e4ff688fc1130f8d8909ea09bc137d668";
const SCALLOP_X_ORACLE = "0x93d5bf0936b71eb27255941e532fac33b5a5c7759e377b4923af0a1359ad494f";

const txb = new TransactionBlock();
txb.setSender();
const [repaySui] = txb.splitCoins(txb.gas, [1e9]);

// Before doing this transaction make sure you have updated the price of our x_oracle
const withdrawSui = txb.moveCall({
  target: "0xa45b8ffca59e5b44ec7c04481a04cb620b0e07b2b183527bca4e5f32372c5f1a::liquidate::liquidate",
  arguments: [
    txb.object(SCALLOP_VERSION_OBJECT),
    obligationId,
    txb.object(SCALLOP_MARKET_OBJECT),
    repaySui,
    txb.object(SCALLOP_COIN_DECIMAL_REGISTRY),
    txb.object(SCALLOP_X_ORACLE),
    txb.object(SUI_CLOCK_OBJECT_ID)
  ],
  typeArguments: ["0x2::sui::SUI", "0x5d4b302506645c37ff133b98c4b50a5ae14841659738d6d733d59d0d217a93bf::coin::COIN"]
});

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

Check here the example how to do update price `x_oracle`&#x20;

{% embed url="https://github.com/scallop-io/sui-scallop-sdk/blob/main/src/builders/oracle.ts" %}

We recommend you to call this function using our [Scallop SDK](https://github.com/scallop-io/sui-scallop-sdk), so before calling any function related to liquidation, you need to call update price in the beginning of the [PTB (Programmable Transaction Block)](https://docs.sui.io/guides/developer/sui-101/building-ptb).

Here what your PTB should looks like:

```rust
PTB for calling function that have to run liquidate function:
- update price (you get this from SDK)
- your function that call liquidate
```
