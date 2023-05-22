# Liquidations

## Summary

The [multi-oracle consensus](oracles.md#aggregate-multi-oracle-strategy)[ algorithm ](oracles.md#aggregate-multi-oracle-strategy)we designed allows Scallop to obtain price feeds through a multi-oracle system. In the event of detecting an unhealthy asset portfolio, Scallop can accurately and promptly identify liquidation events. The integration of our permissionless liquidation system with **DeepBook**, **Cetus**, **Turbos**, and **Umi Protocol** offers seamless compatibility.

As your Health Bar approaches 100%, your account becomes susceptible to potential liquidation. The Liquidation Threshold represented is determined by specific token parameters. We calculate the liquidation threshold by considering the weighted average of all the assets you have deposited.

#### **Scallop Liquidation BOT Github Repo:**

[**https://github.com/scallop-io/sui-scallop-liquidator**](https://github.com/scallop-io/sui-scallop-liquidator)

## Liquidation Scenario

Consider a hypothetical scenario where Sarah provides $12,500 USDC and borrows $9,800 worth of ETH. If the value of ETH increases by 7.85% to approximately $10,600, Sarah's account becomes eligible for liquidation.

In this liquidation event, the liquidator repays 18% of the ETH loan, which amounts to $1,764. Additionally, the liquidator collects $1,764 from the collateral USDC supply to cover the borrowed ETH. As a bonus for successfully completing the liquidation, the liquidator also receives an additional 9% ($158).

After the liquidation process, Sarah is left with $10,738 in USDC ($12,500 - $1,764 - $158) and $8,836 in borrowed ETH ($10,600 - $1,764). The liquidator, on the other hand, paid $1,764 in ETH and received $1,922 in USDC, resulting in a profit of $158.

As a result of the liquidation, Sarah's Liquidation Threshold decreases from 80% to 77%, indicating the impact on her account's risk exposure, while ensuring the specific numerical values are different from the original example.
