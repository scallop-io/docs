# Liquidation

## Introduction

Liquidation occurs when a borrower’s collateral value falls below the required threshold to secure their loan. This can happen due to a decrease in the collateral’s value or an increase in the value of the borrowed asset.

Before diving into how the liquidation mechanism works in Scallop, it’s essential to understand the key concepts behind liquidation on the platform. Scallop’s approach is designed to minimize the impact on borrowers while ensuring the protocol’s stability through efficient, precise, and user-friendly liquidation processes.

## Soft Liquidation

Unlike other protocols, where a user’s position becomes unhealthy and liquidators working with the protocol automatically sell all of the user’s collateral to repay the borrower’s debt, Scallop takes a more user-friendly approach.

In Scallop, liquidators only sell the necessary amount of collateral to cover the user’s debt that exceeds the threshold. This ensures the user’s position returns to a healthy state. If the position still remains unhealthy even after partial repayment, the liquidation process will continue incrementally until the user’s position is fully restored to a healthy status.

This approach minimizes the impact on users, preserving as much of their collateral as possible while maintaining the integrity of the lending protocol.

## Risk Level

Risk Level acts as a threshold indicator. A Risk Level below 100% means the borrower’s position is safe, while a Risk Level of 100% or higher signals that the borrower’s debt has exceeded the safe limit, triggering the possibility of liquidation to protect the protocol’s stability. This metric provides a clear and actionable way for users to monitor their borrowing status and manage risks effectively.

<figure><img src="../.gitbook/assets/image (105).png" alt=""><figcaption><p>Obligation Portfolio</p></figcaption></figure>

So, you might be curious about how Scallop calculates the value of this Risk Level. This is how we calculate the risk level :

**Borrower's Collateral**

| Coin Name | Price | Deposit | Liquidation Factor |
| --------- | ----- | ------- | ------------------ |
| USDC      | $1    | 1000    | 90%                |
| SUI       | $1    | 500     | 80%                |

{% hint style="info" %}
Total Collateral Value: $1,500

Required Collateral Value: $1,300
{% endhint %}

**Borrower's Current Debt**

| Coin Name | Price | Borrowed | Borrow Weight |
| --------- | ----- | -------- | ------------- |
| SCA       | $0.5  | 1000     | 100%          |
| USDT      | $1    | 500      | 100%          |

{% hint style="info" %}
Borrow value with weight: $1,000

Risk Level = Borrow Value with Weight / Required Collateral Value

Current Risk Level: 76%
{% endhint %}

This example demonstrates how Scallop calculates the risk level.

## Liquidation parameter

Here are the key liquidation parameters applied to borrowers undergoing liquidation on Scallop:

### Liquidation Penalty

Borrowers subject to liquidation incur a penalty, which varies depending on the specific lending pool. This penalty is applied when the borrower’s collateral is sold. For instance, if the liquidation penalty is 10% and $100 of collateral is sold, $90 will be used to repay the borrower’s debt, while the remaining $10 is allocated to the Liquidation Reserve Factor.

### Liquidation Reseve Factor

The Liquidation Reserve Factor is the portion of the liquidation penalty directed to Scallop’s treasury. For example, if the liquidation penalty is 10% and the liquidation reward is 5%, liquidators will pay $95 for $100 worth of collateral. Of this amount, $90 is used to repay the borrower’s debt, while $5 goes to the treasury as part of the reserve factor.

### Liquidation Reward

To encourage participation in the liquidation process, Scallop rewards liquidators who repay outstanding loans and acquire the borrower’s collateral at a discount. For example, with a 5% liquidation reward, liquidators can purchase the collateral at 95% of its market value, incentivizing timely and efficient liquidation actions.

### Liquidation Factor

The **liquidation factor** sets a threshold for how much debt a user can take against their collateral.

{% hint style="info" %}
Example:

Liquidation Factor SUI: 0.8 (80%) Liquidation Factor USDC: 0.9 (90%)

if a user has collateral consisting of **100 USDC** and **200$ value of SUI**, the liquidation thresholds are calculated as follows:

* **USDC**: $100 \* 0.9 (90% liquidation factor) = **$90**
* **SUI**: $200 \* 0.8 (80% liquidation factor) = **$160**

This gives a total collateral value of **$250**. If the user’s debt exceeds **$250**, they become eligible for liquidation.
{% endhint %}

## Liquidation Scenario

In a hypothetical scenario, Kris provided $10,000 in USDC as collateral and borrowed $8,500 worth of SUI (with a collateral factor of 85% for USDC). If the value of SUI increases by 6% in a short period, reaching approximately $9,010, the risk level (debt amount / collateral \* liquidation factor) rises from 94.4% ($8,500 / $10,000 \* 90%) to 100.1% ($9,010 / $10,000 \* 90%). At this point, Kris's account will trigger soft liquidation to reduce the risk level back to 100%.

In this liquidation event, the liquidator repaid approximately 11% of the borrower’s SUI debt, amounting to $1,000, reducing the debt to $8,010. A total of $1,100 in USDC collateral was liquidated, which included debt repayment, a liquidation reserve (5%), and a liquidation reward (5%).

After the liquidation, Kris was left with $8,900 in USDC ($10,000 - $1,100) and $8,010 in outstanding SUI debt ($9,010 - $1,000). On the other hand, the liquidator paid $1,000 worth of SUI and received $1,050 in USDC, earning a profit of $50.

Due to the liquidation, Kris’s liquidation threshold (risk level) decreased from 100.1% to 100%. If the price of SUI rises again, further liquidations will continue to be triggered to maintain the risk level at 100%.

## Liquidation Guidelines

Under specific circumstances, liquidation will occur when a borrower's risk level exceeds 100% due to insufficient deposit or collateral value to cover their loan. This situation arises when the value of deposited collateral decreases or the borrowed debt value increases relative to each other.

To avoid liquidation, it is crucial to maintain awareness of your risk level and ensure sufficient margin in your account. If your risk level rises unexpectedly, you can mitigate it by increasing your collateral assets or repaying your loan. Additionally, you can use our integrated feature which will give your notification when your risk level already exceeds certain level. You can read this page [How to Avoid Liquidation](../scalloper-guide/how-to-avoid-liquidation.md) to get guide setup the notification.

Scallop’s soft liquidation mechanism aims to ensure that lenders are protected even if the value of the collateral decreases. It also provides an opportunity for borrowers to rectify the situation before their collateral is fully liquidated, minimizing their losses.

It's important to note that the specific details of Scallop’s liquidation mechanism may be subject to change or updates. It's always recommended to follow up with the latest announcement on the changes of the protocol.
