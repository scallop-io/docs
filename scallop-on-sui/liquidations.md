# Liquidations

## Summary

The [multi-oracle consensus](oracles.md#aggregate-multi-oracle-strategy)[ algorithm ](oracles.md#aggregate-multi-oracle-strategy)we designed allows Scallop to obtain price feeds through a multi-oracle system. In the event of detecting an unhealthy asset portfolio, Scallop can accurately and promptly identify liquidation events. The integration of our permissionless liquidation system with **DeepBook**, **Cetus**, **Turbos**, and **Umi Protocol** offers seamless compatibility.

As your Risk Level approaches 100%, your account becomes susceptible to potential liquidation. The Liquidation Threshold represented is determined by specific token parameters. We calculate the liquidation threshold by considering the weighted average of all the assets you have deposited.

#### **Scallop Liquidation BOT Github Repo:**

[**https://github.com/scallop-io/sui-scallop-liquidator**](https://github.com/scallop-io/sui-scallop-liquidator)

## Soft Liquidations

Scallop employs a dynamic close factor to facilitate what we refer to as "soft liquidations." Specifically, liquidators are permitted to repay an amount that brings a violator back into compliance, plus an additional safety factor. Consequently, borrowers who are only marginally in violation will often have significantly less than half of their debts repaid during a liquidation. Conversely, heavily violative borrowers may see a substantial portion or the entirety of their debts repaid, depending on the circumstances surrounding the liquidation process.

## Liquidation Scenario

Consider a hypothetical scenario where Kris provides $12,500 USDC and borrows $9,800 worth of wETH. If the value of wETH increases by 7.85% to approximately $10,600, Kris's account becomes eligible for liquidation.

In this liquidation event, the liquidator repays 18% of the wETH loan, which amounts to $1,764. Additionally, the liquidator collects $1,764 from the collateral USDC supply to cover the borrowed wETH. As a bonus for successfully completing the liquidation, the liquidator also receives an additional 9% ($158).

After the liquidation process, Kris is left with $10,738 in USDC ($12,500 - $1,764 - $158) and $8,836 in borrowed wETH ($10,600 - $1,764). The liquidator, on the other hand, paid $1,764 in wETH and received $1,922 in USDC, resulting in a profit of $158.

As a result of the liquidation, Kris's Liquidation Threshold decreases from 80% to 77%, indicating the impact on his account's risk exposure, while ensuring the specific numerical values are different from the original example.\


## Liquidation Guidelines

Under specific circumstances, liquidation will occur when a borrower's risk level exceeds 100% due to insufficient deposit or collateral value to cover their loan. This situation arises when the value of deposited collateral decreases or the borrowed debt value increases relative to each other.

To avoid liquidation, it is crucial to maintain awareness of your risk level and ensure sufficient margin in your account. If your risk level rises unexpectedly, you can mitigate it by increasing your collateral assets or repaying your loan. Additionally, you will soon have the option to subscribe to notifications within our app, allowing you to track and receive alerts via email or SMS when your deposits are at risk.\
