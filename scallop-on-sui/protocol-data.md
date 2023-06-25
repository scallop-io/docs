# Scallop Money Market Protocol Data

## Asset Types

| Asset name | Asset type                                                                     |
|------------|--------------------------------------------------------------------------------|
| USDC       | 0x5d4b302506645c37ff133b98c4b50a5ae14841659738d6d733d59d0d217a93bf::coin::COIN |
| SUI        | 0x2::sui::SUI                                                                  |

## Interest Rate Models
Scallop adopts a tri-linear interest rate model. The interest rate for borrow goes higher as the utilization rate increases.

| Asset name | 0% utilization | 60% utilization | 80% utilization | 100% utilization |
|------------|----------------|-----------------|-----------------|------------------|
| USDC       | 3%             | 8%              | 50%             | 100%             |
| SUI        | 5%             | 10%             | 50%             | 200%             |

## Risk Models
Scallop defines a risk model for each collateral asset. The risk model is used to calculate the collateral ratio for each collateral asset.

| Asset name | Collateral factor | Liquidation factor | Liquidation penalty | Liquidation discount |
|------------|-------------------|--------------------|---------------------|----------------------|
| USDC       | 80%               | 90%                | 5%                  | 4%                   |
| SUI        | 60%               | 80%                | 5%                  | 4%                   |

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

| Asset name    | Borrow weight |
|---------------|---------------|
| wormhole_usdc | 1             |
| sui           | 1.25          |

## Outflow limit
Outflow limit is used to limit the amount of tokens that can be borrowed during a period of time.
For example, if the outflow limit of USDC is 1,000,000, then the total amount of USDC that can be borrowed in 24 hours is 1000000.

| Asset name    | Outflow limit | Time period |
|---------------|---------------|-------------|
| wormhole_usdc | 1,000,000     | 24 hours    |
| sui           | 1,000,000     | 24 hours    |
