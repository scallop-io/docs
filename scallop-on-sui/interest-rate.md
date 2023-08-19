# Interest Rates

## Dynamics Interest Rate

At Scallop, interest rates for borrowing are determined by static linear (or piecewise linear) models. In a general sense, as the demand for borrowing rises or the supply diminishes, interest rates experience an upward trend. Conversely, when the supply increases or the demand for borrowing declines, interest rates decrease accordingly.

## Upgradable Protocol Parameters

The smart contracts on Sui are upgradeable, and the Scallop Protocol encompasses interest rate models, liquidation parameters, oracle integrations, and asset pools. These components undergo periodic upgrades and adjustments based on market conditions, strategic considerations, and protocol optimizations. As the governance infrastructure on the Sui chain matures, the governance authority will be gradually transitioned to the community through decentralized governance using tokens.

## Trilinear Interest Rate Model

Unlike Compound's dual-line interest rate model, the Trilinear model for Scallop works in three distinct phases, each triggered by different levels of capital utilization. When capital utilization nears its upper limit, the system ensures liquidity providers are adequately compensated for the heightened risk, while borrowers are signaled to reduce their positions due to increased borrowing costs. The Trilinear Interest Rate Model for Scallop is specifically designed to cater to the dynamic needs of the decentralized finance space, optimizing the stability of interest rates and responsiveness to market conditions.

## Scallop Interest Rate Model

{% embed url="https://docs.google.com/spreadsheets/d/1Z3uGcwG1eYm-ulVGgFpjA4USYjh8bBLxx98ZW24b3HM/edit?usp=sharing" %}
