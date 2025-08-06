# Isolated Asset

We are thrilled to announce the launch of Isolated Asset Pools on Scallop, this new feature is Scallop’s next step towards providing more features for our users, making Scallop an All-In-One platform to onboard the next millions of users.

<figure><img src="../.gitbook/assets/截圖 2024-12-23 下午10.07.41.png" alt=""><figcaption></figcaption></figure>

## What are Isolated Assets?

The isolated asset feature limits risks to a specific pool, ensuring bad debt doesn’t affect others.

This allows the protocol to support more diverse assets without cross-pool risk.

An obligation with isolated asset debt cannot coexist with other debts, allowing only one type of isolated asset to be borrowed at a time.

## Difference between non-Isolated Assets and Isolated Assets

Borrowing isolated assets requires a higher collateral ratio, typically **200%**. This means you must provide collateral worth at least twice the amount you wish to borrow. Additionally, isolated assets have a borrowing fee of **1%**, higher than that of non-isolated assets.

## The best way to Borrow Isolated Assets

In order to borrow isolated assets, users have to first deposit collateral assets. For a single obligation key, users will not be able to borrow any other assets if they have borrowed an isolated asset.

{% hint style="info" %}
For Example:

Alice has deposited multiple collateral (USDC, USDT)\
After Alice has borrowed isolated asset $FUD, Alice cannot borrow any other asset like SUI, ETH or even $DEEP (which also isolated asset).

To be able to borrow other asset，Alice need to repay all of her $FUD debt to be able to borrow other assets including $DEEP.&#x20;
{% endhint %}

## The best way to borrow Isolated Assets

The best way to borrow Isolated asset is using **multiple obligations**, by simply creating new obligation you won't have to do anything with your existing positions.

<figure><img src="../.gitbook/assets/截圖 2024-12-23 下午9.59.49 (1).png" alt=""><figcaption></figcaption></figure>

Once you created, you can see your new obligation and existing ones and switch between them. After depositing collateral asset in new obligation, you can borrow the Isolated Assets.

<figure><img src="../.gitbook/assets/截圖 2024-12-23 下午10.11.30.png" alt=""><figcaption></figcaption></figure>

## Supply and Borrow Isolated Assets Today

Scallop is very excited to bring in more diverse assets onto our protocol for our users. Stay tuned for more isolated asset listings on Scallop!
