# Scallop Money Market Protocol Data

## Asset Types

| Asset name | Asset type                                                                       |
|------------|----------------------------------------------------------------------------------|
| wUSDC      | 0x5d4b302506645c37ff133b98c4b50a5ae14841659738d6d733d59d0d217a93bf::coin::COIN   |
| wUSDT      | 0xc060006111016b8a020ad5b33834984a437aaa7d3c74c18e09a95d48aceab08c::coin::COIN   |
| wETH       | 0xaf8cd5edc19c4512f4259f0bee101a40d41ebed738ade5874359610ef8eeced5::coin::COIN   |
| SUI        | 0x2::sui::SUI                                                                    |
| CETUS      | 0x06864a6f921804860930db6ddbe2e16acdf8504495ea7481637a1c8b9a8fe54b::cetus::CETUS |
| afSUI      | 0xf325ce1300e8dac124071d3152c5c5ee6174914f8bc2161e88329cf579246efc::afsui::AFSUI |
| haSUI      | 0xbde4ba4c2e274a60ce15c1cfff9e5c42e41654ac8b6d906a57efa4bd3c29f47d::hasui::HASUI |

## Interest Rate Models
Scallop adopts a tri-linear interest rate model. The interest rate for borrow goes higher as the utilization rate increases.

| Asset name | 0% utilization | 60% utilization | 90% utilization | 100% utilization |
|------------|----------------|-----------------|-----------------|------------------|
| wUSDC      | 0%             | 8%              | 50%             | 150%             |
| wUSDT      | 0%             | 8%              | 50%             | 150%             |
| wETH       | 0%             | 10%             | 100%            | 300%             |
| SUI        | 0%             | 10%             | 100%            | 300%             |
| CETUS      | 0%             | 10%             | 100%            | 300%             |
| afSUI      | 0%             | 10%             | 100%            | 300%             |
| haSUI      | 0%             | 10%             | 100%            | 300%             |

## Risk Models
Scallop defines a risk model for each collateral asset. The risk model is used to calculate the collateral ratio for each collateral asset.

| Asset name | Collateral factor | Liquidation factor | Liquidation penalty | Liquidation discount | Max collateral amount |
|------------|-------------------|--------------------|---------------------|----------------------|-----------------------|
| wUSDC      | 80%               | 90%                | 5%                  | 4%                   | 10,000,000            |
| wUSDT      | 80%               | 90%                | 5%                  | 4%                   | 10,000,000            |
| wETH       | 70%               | 80%                | 5%                  | 4%                   | 10,000                |
| SUI        | 70%               | 80%                | 5%                  | 4%                   | 20,000,000            |
| CETUS      | 30%               | 80%                | 5%                  | 4%                   | 1,000,000             |
| afSUI      | 60%               | 70%                | 10%                 | 8%                   | 100,000               |
| haSUI      | 60%               | 70%                | 10%                 | 8%                   | 100,000               |

### Parameter explanation:

**Collateral factor**

The collateral ratio for this asset.
For example, if your collateral is worth 100$, and the collateral factor is 80%, then you can borrow up to 80$ of debt.

**Liquidation factor**

The collateral ratio for this asset when it is under liquidation.
For example, if your collateral is worth 100$, and the liquidation factor is 90%, then your collateral will be liquidated when your debt is greater than 90$.

**Liquidation penalty**

The penalty for unhealthy loan. It happens when you don't repay in time when your collateral value drop to unhealthy level.
For example, if you have an unhealthy loan, and the liquidation penalty is 5%, then part of your collaterals will be sold at 95% of market price.

**Liquidation discount**

The discount for liquidators.
For example, if the liquidation discount is 4%, then liquidators can buy your collaterals at 96% of market price.
The gap between liquidation penalty and liquidation discount goes to the Scallop treasury.

## Borrow weight
Borrow weight is used to calculate the amount of debt a user can borrow.

For example:
- You have 100$ of USDC collateral, and collateral factor is 80%
- You want to borrow SUI, price of SUI is 2$, borrow weight of SUI is 1.25
- The you can borrow up to: 100 * 80% / (2 * 1.25) = 32 SUI

| Asset name | Borrow weight |
|------------|---------------|
| wUSDC      | 1             |
| wUSDT      | 1             |
| wETH       | 1             |
| SUI        | 1             |
| CETUS      | 1             |
| afSUI      | 1             |
| haSUI      | 1             |

## Outflow limit
Outflow limit is used to limit the amount of tokens that can be borrowed during a period of time.
For example, if the outflow limit of USDC is 1,000,000, then the total amount of USDC that can be borrowed in 24 hours is 1000000.

| Asset name | Outflow limit | Time period |
|------------|---------------|-------------|
| wUSDC      | 1,000,000     | 24 hours    |
| wUSDT      | 1,000,000     | 24 hours    |
| wETH       | 1,000         | 24 hours    |
| SUI        | 1,000,000     | 24 hours    |
| CETUS      | 1,000,000     | 24 hours    |
| afSUI      | 10,000        | 24 hours    |
| haSUI      | 10,000        | 24 hours    |
