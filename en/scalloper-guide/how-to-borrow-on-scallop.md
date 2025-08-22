# How to Borrow on Scallop

## Borrow

To borrow on Scallop, you need to deposit collateral so that you can borrow the desired asset. However, before making the deposit and borrowing, you need to create an [obligation](broken-reference) account.

<figure><img src="../.gitbook/assets/image (7).png" alt="" width="563"><figcaption><p>Create obligation account</p></figcaption></figure>

### Deposit Collateral

You can choose the asset that you want to use as collateral.

<figure><img src="../.gitbook/assets/image (10).png" alt="" width="563"><figcaption><p>Collateral Pools</p></figcaption></figure>

Enter the amount of assets you want to use as collateral.

<figure><img src="../.gitbook/assets/image (9).png" alt="" width="375"><figcaption><p>Deposit SUI collateral</p></figcaption></figure>

> You will not earn any yield on assets that you use as collateral.

<figure><img src="../.gitbook/assets/image (11).png" alt="" width="563"><figcaption><p>Deposited Assets</p></figcaption></figure>

As seen in the image above, you can view a summary dashboard of the assets you've deposited in the collateral pools. The summary dashboard consists of four sections:

1. **Available Collateral**: Total USD value of assets available for borrowing.
2. **Deposited Collateral**: Total USD value of assets deposited into the Collateral Pools.
3. **Risk Level**: Indicates the security status of the obligation account, calculated as "borrowValueWithWeight" divided by "requireCollateralValue". A reading of 100% means the liquidation threshold is reached, even if it exceeds this value.
4. **Collateral Portfolio**: Lists the assets you've supplied to the collateral pools.

### Borrowing

After depositing your assets into the collateral pools, you can select the assets you want to borrow from the borrowing pools. Enter the amount you want to borrow from the borrowing pools, and consider that the higher your borrowing amount, the higher the Risk Level of your obligation, which may lead to your obligation account being liquidated.

<figure><img src="../.gitbook/assets/image (12).png" alt="" width="563"><figcaption><p>Borrow Assets</p></figcaption></figure>

As seen in the image above, there are **Borrow Fee** parameters, meaning you will be charged a fee of 0.3% every time you borrow assets.

<figure><img src="../.gitbook/assets/image (13).png" alt="" width="563"><figcaption><p>Borrow Dashboard</p></figcaption></figure>

* **Available Collateral**: Total USD assets that you can borrow.
* **Debt Assets**: Total USD assets that you have borrowed.
* **Risk Level**: Indicates the security status of your obligation account, calculated based on "borrowValueWithWeight" divided by "requireCollateralValue". A reading of 100% indicates that the liquidation threshold has been reached; it remains at 100% even if exceeded.&#x20;
* **Debt Portfolio**: List of assets that you have borrowed.

#### Borrow APR and Reward APR

You may notice that in the borrowing pools, there are columns for Borrow APR and Reward APR.

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption><p>Borrowing Pools</p></figcaption></figure>

Borrow APR refers to the loan interest rate, while Reward APR is the incentive program provided to users who borrow. When the Reward APR is greater than the Borrow APR, it means that by borrowing, you receive a positive yield.

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption><p>Claim Incentive Reward</p></figcaption></figure>

You can claim rewards from borrowing in that panel as well. So, if you stake your sCoins and also borrow assets with a reward APR, it means you receive Reward Incentive Program from both the Lending Pools and Borrowing Pools.

### Avoid Liquidation

To avoid liquidation, you can set the Risk Level of your obligation to be less than 100%. If the Risk Level of your obligation account exceeds 100%, Scallop will initiate the [Soft Liquidation](broken-reference) mechanism.

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption><p>Borrowing Dashboard</p></figcaption></figure>

In the example, the obligation has reached 93%, and if it surpasses 100%, our collateral assets will be liquidated. To prevent this, we can repay the assets we previously borrowed. Since the borrowed assets are only USDC, we can repay this asset to decrease the Risk Level percentage.

<figure><img src="../.gitbook/assets/image (17).png" alt="" width="375"><figcaption><p>Repay Debt</p></figcaption></figure>

After repaying the debt assets, our Risk Level percentage has decreased.

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption><p>Borrowing Dashboard</p></figcaption></figure>

#### Withdraw Collateral

Before withdrawing collateral, make sure you have repaid all the assets you borrowed along with their interest. Once you have repaid all the debt assets, you can withdraw all your assets from the collateral pools.

<figure><img src="../.gitbook/assets/image (21).png" alt="" width="375"><figcaption><p>Withdraw Collateral</p></figcaption></figure>

Visit [Borrowing](broken-reference) and [Liquidation](broken-reference) to get more information
