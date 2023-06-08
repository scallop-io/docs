# Liquidations

## Summary

The [multi-oracle consensus](oracles.md#aggregate-multi-oracle-strategy)[ algorithm ](oracles.md#aggregate-multi-oracle-strategy)we designed allows Scallop to obtain price feeds through a multi-oracle system. In the event of detecting an unhealthy asset portfolio, Scallop can accurately and promptly identify liquidation events. The integration of our permissionless liquidation system with **DeepBook**, **Cetus**, **Turbos**, and **Umi Protocol** offers seamless compatibility.

As your Risk Level approaches 100%, your account becomes susceptible to potential liquidation. The Liquidation Threshold represented is determined by specific token parameters. We calculate the liquidation threshold by considering the weighted average of all the assets you have deposited.

#### **Scallop Liquidation BOT Github Repo (Not open-sourced yet):**

[**https://github.com/scallop-io/sui-scallop-liquidator**](https://github.com/scallop-io/sui-scallop-liquidator)

## Soft liquidation

Scallop utilizes a soft liquidation mechanism to protect lenders and borrowers. Here's how scallop implements the soft liquidation process:

### Collateral Factor

Scallop maintains a specific collateral factor for each asset. For example, if the collateral factor for BTC is set at 70%, borrower who has 100$ worth of BTC can have at max 70$ in debt.

### Liquidation Threshold

Scallop protocol constantly monitors the value of the collateral. If the value of the collateral falls below a certain threshold, a soft liquidation process is triggered.

### Liquidation reward
To incentivize users to participate in the liquidation process, Scallop offers rewards to liquidators who repay outstanding loans and obtain the borrower's collateral at a discounted price. For example, liquidators can obtain the collateral at 95% of market price, when the liquidation reward is set to 5%

### Borrower Notification
Once the collateral falls below the threshold, Scallop initiates a grace period where the borrower is notified of the low collateral value and given a chance to increase their collateral or repay the loan to avoid liquidation.


### Soft Liquidation
If the borrower doesn't take corrective action during the grace period, Scallop begins the gradual liquidation process. It automatically starts selling a portion of the borrower's collateral on the market to repay the lender's loan. The liquidation process continues until the loan is fully repaid or the collateral value exceeds the required threshold.

### Liquidation Penalty
Scallop imposes a liquidation penalty on borrowers whose collateral is liquidated. This penalty is cut off when selling the borrower’s collateral. For example, if the liquidation penalty is 10%, then selling 100$ of collaterals, 90$ are used to payback the borrower’s debt.

### Liquidation Reserve Factor
When doing the liquidation, The liquidation penalty is usually bigger than liquidation reward. Let’s say, liquidation penalty is 10%, liquidation reward is 5%, it means liquidations pay 95$ for 100$ worth of collaterals. 90$ will be used to repay debt, 5$ will go to scallop treasury. So the liquidation reserve factor is 5%.


## Liquidation Scenario

Consider a hypothetical scenario where Kris provides $12,500 USDC and borrows $9,800 worth of wETH. If the value of wETH increases by 7.85% to approximately $10,600, Kris's account becomes eligible for liquidation.

In this liquidation event, the liquidator repays 18% of the wETH loan, which amounts to $1,764. Additionally, the liquidator collects $1,764 from the collateral USDC supply to cover the borrowed wETH. As a bonus for successfully completing the liquidation, the liquidator also receives an additional 9% ($158).

After the liquidation process, Kris is left with $10,738 in USDC ($12,500 - $1,764 - $158) and $8,836 in borrowed wETH ($10,600 - $1,764). The liquidator, on the other hand, paid $1,764 in wETH and received $1,922 in USDC, resulting in a profit of $158.

As a result of the liquidation, Kris's Liquidation Threshold decreases from 80% to 77%, indicating the impact on his account's risk exposure, while ensuring the specific numerical values are different from the original example.\


## Liquidation Guidelines

Under specific circumstances, liquidation will occur when a borrower's risk level exceeds 100% due to insufficient deposit or collateral value to cover their loan. This situation arises when the value of deposited collateral decreases or the borrowed debt value increases relative to each other.

To avoid liquidation, it is crucial to maintain awareness of your risk level and ensure sufficient margin in your account. If your risk level rises unexpectedly, you can mitigate it by increasing your collateral assets or repaying your loan. Additionally, you will soon have the option to subscribe to notifications within our app, allowing you to track and receive alerts via email or SMS when your deposits are at risk.\

Scallop’s soft liquidation mechanism aims to ensure that lenders are protected even if the value of the collateral decreases. It also provides an opportunity for borrowers to rectify the situation before their collateral is fully liquidated, minimizing their losses.

It's important to note that the specific details of Scallop’s liquidation mechanism may be subject to change or updates. It's always recommended to follow up with the latest announcement on the changes of the protocol.
