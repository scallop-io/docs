# Liquidation

### Overview

Unlike many lending protocols where liquidators can sell off all of a user's collateral at once, Scallop takes a more user-friendly approach. Scallop uses a **soft liquidation** mechanism where liquidators only repay up to **20% of a borrower's total debt** per liquidation call, and receive a portion of the borrower's collateral at a discount in return. This gradual process minimizes the impact on borrowers, preserving as much of their collateral as possible while keeping the protocol solvent.

If a position still remains unhealthy after a partial liquidation, the process can be repeated incrementally until the borrower's position is fully restored to a healthy status.

### When Does Liquidation Happen?

<figure><img src="../.gitbook/assets/image (107).png" alt=""><figcaption></figcaption></figure>

Scallop evaluates each borrower's position by comparing two values:

* **Weighted Debt Value**: the total USD value of everything you've borrowed, adjusted by each asset's `borrow_weight`. Assets with higher borrow weights count for more against your position.
* **Collateral Value for Liquidation**: the total USD value of your deposited collateral, adjusted by each asset's `liquidation_factor`. This determines how much borrowing your collateral can support before liquidation.

Your **Risk Level** reflects the ratio between these two values. A Risk Level below 100% means your position is safe. When your Risk Level reaches or exceeds 100%, your weighted debt value has surpassed your collateral value for liquidation, and your position becomes open to liquidation.

Each asset on Scallop has its own risk parameters, so the composition of your collateral and debt matters. For example, borrowing a high `borrow_weight` asset against a low `liquidation_factor` collateral puts you closer to the liquidation threshold than a more conservative pairing.

### Soft Liquidation

Scallop's soft liquidation mechanism is designed to protect borrowers from losing their entire collateral in a single event.

**How it works:**

* Each liquidation call can repay a maximum of **20% of the borrower's total debt value** (across all debt types). This cap prevents excessive collateral loss from a single liquidation.
* If the position is still unhealthy after one liquidation, additional liquidation calls can follow, each limited to 20% of the remaining total debt, until the position returns to health.
* For very small positions (total debt under **$10**), the full debt can be repaid in a single call. These "dust" positions are too small to liquidate incrementally in an economical way.

This step-by-step approach significantly reduces the risk of cascading bad debt, where one large liquidation could destabilize a position further.

### Liquidation Penalties and Rewards

When a liquidation occurs, the borrower's collateral is seized and distributed between the liquidator and the protocol:

**For the borrower:** You incur a **liquidation penalty** on the collateral that is seized. The penalty rate varies by collateral type and is set by governance, with a maximum of 20%. This means if you are liquidated, you lose slightly more collateral than the debt that was repaid on your behalf.

**For the liquidator:** Liquidators are rewarded with a **liquidation discount**, meaning they receive the borrower's collateral at a price below market value. For example, with a 5% liquidation discount, a liquidator effectively purchases $100 worth of collateral for $95 worth of debt repayment. The maximum discount is 15%.

**For the protocol:** The difference between the liquidation penalty and the liquidation discount flows to the protocol as revenue. For instance, if the penalty is 8% and the discount is 5%, the protocol captures 3% of the seized collateral value.

The key parameters per collateral type are:

<table><thead><tr><th>Parameter</th><th width="480.265625">What It Means</th><th>Maximum</th></tr></thead><tbody><tr><td>Liquidation Factor</td><td>How much of your collateral's value counts toward the liquidation threshold. Higher = more room before liquidation.</td><td>95%</td></tr><tr><td>Liquidation Discount</td><td><p>The discount liquidators receive on your collateral. </p><p>Higher = more incentive for liquidators.</p></td><td>15%</td></tr><tr><td>Liquidation Penalty</td><td><p>The total penalty applied to your seized collateral. </p><p>The penalty is always ≥ the discount.</p></td><td>20%</td></tr></tbody></table>

Note that the borrower's debt is reduced by the **full repayment amount**. The protocol's revenue share comes from the collateral side, not from the debt repayment. This means borrowers benefit from maximum debt reduction on every liquidation.

### Who Can Liquidate?

Liquidation on Scallop is **permissionless**. Anyone can liquidate an unhealthy position. There is no whitelist or special access required. This open design ensures that unhealthy positions are addressed promptly, keeping the protocol solvent.

Liquidators typically run automated bots that monitor positions and execute liquidations when profitable. If you're interested in running a liquidation bot, refer to the [Liquidation Function](https://docs.scallop.io/integrations/contract-integration/liquidation-function) integration guide for technical details.

### How to Avoid Liquidation

You can protect yourself from liquidation by actively managing your position:

* **Monitor your Risk Level** on the Scallop dashboard. When your weighted debt approaches your liquidation-weighted collateral value, you're at risk.
* **Add more collateral** to increase the buffer between your debt and the liquidation threshold.
* **Repay part of your debt** to reduce your weighted debt value.
* **Be mindful of asset selection.** Collateral assets with higher liquidation factors give you more breathing room, while borrowed assets with higher borrow weights push you closer to the threshold.
* **Watch for market movements.** A drop in collateral price or a rise in debt token price can push you toward liquidation even if you haven't changed your position.
