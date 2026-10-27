# Querying Pool Data

Use **`ScallopQuery`** to read market data such as pool APYs, utilization, collateral factors, flash loan fees and total value locked. These methods do not need a `secretKey`.

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
By default the data is read from the Scallop API first, and falls back to the chain if the API fails. Cached results are reused for a short time, so repeated calls are cheap. Prefer fetching all pools once and reusing the result, instead of calling per coin.
{% endhint %}

## Get Market Pools

Returns the lending pools and the collaterals of the given coins, keyed by coin name. If no coin is given, all whitelisted lending pools are returned.

```typescript
const { pools, collaterals } = await scallopQuery.getMarketPools();

const sui = pools.sui;
console.log(sui?.supplyApy); // supply APY
console.log(sui?.borrowApy); // borrow APY
console.log(sui?.utilizationRate);
console.log(sui?.supplyCoin); // total supplied, in coin unit
console.log(sui?.borrowCoin); // total borrowed, in coin unit
console.log(sui?.coinPrice);
```

To get a single pool:

```typescript
const usdcPool = await scallopQuery.getMarketPool('usdc');
```

### Main Fields of `MarketPool`

| Field                             | Description                                             |
| --------------------------------- | ------------------------------------------------------- |
| `supplyApr` / `supplyApy`         | Current supply rate                                     |
| `borrowApr` / `borrowApy`         | Current borrow rate                                     |
| `utilizationRate`                 | Borrowed amount divided by supplied amount              |
| `supplyCoin` / `borrowCoin`       | Total supplied / borrowed, in coin unit                 |
| `maxSupplyCoin` / `maxBorrowCoin` | Pool supply / borrow limit, in coin unit                |
| `conversionRate`                  | Exchange rate between the sCoin and the underlying coin |
| `borrowFee`                       | Fee charged when borrowing                              |
| `minBorrowAmount`                 | Minimum amount of one borrow                            |
| `isIsolated`                      | Whether the asset is an isolated asset                  |

## Get Market Collaterals

Returns the collateral parameters of the given coins. If no coin is given, all whitelisted collaterals are returned.

```typescript
const collaterals = await scallopQuery.getMarketCollaterals();

const sui = collaterals.sui;
console.log(sui?.collateralFactor); // borrowing power of the collateral
console.log(sui?.liquidationFactor); // liquidation threshold
console.log(sui?.liquidationPenalty);

// Single collateral
const sca = await scallopQuery.getMarketCollateral('sca');
```

## Get Pool Limits

```typescript
const supplyLimit = await scallopQuery.getPoolSupplyLimit('sui');
const borrowLimit = await scallopQuery.getPoolBorrowLimit('sui');
```

## Get Flash Loan Fees

Returns the fee rate of each asset as a decimal (e.g. `0.0005` is 0.05%).

```typescript
const fees = await scallopQuery.getFlashLoanFees(['sui', 'usdc']);
console.log(fees.sui);
```

## Get Isolated Assets

Isolated assets have extra restrictions when used as collateral or borrowed.

```typescript
const isolatedAssets = await scallopQuery.getIsolatedAssets();
const isIsolated = await scallopQuery.isIsolatedAsset('sca');
```

## Get Total Value Locked

```typescript
const tvl = await scallopQuery.getTvl();
console.log(tvl.supplyValue); // total supplied value (USD)
console.log(tvl.borrowValue); // total borrowed value (USD)
console.log(tvl.totalValue);
```

## Get Coin Prices

```typescript
// All whitelisted coins, keyed by coin name
const prices = await scallopQuery.getAllCoinPrices();

// Pyth prices only
const pythPrice = await scallopQuery.getPythCoinPrice('sui');
```

## Get Borrow Incentive Pools

```typescript
const incentivePools = await scallopQuery.getBorrowIncentivePools();
```
