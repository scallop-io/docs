# Borrowing

## Collateral Assets

The **Collateral Pools** allow borrowers to deposit collateral and obtain a percentage of borrowing capacity, but suppliers cannot earn any interest from the collateral pool. Borrowers who want to borrow from the asset pool must first deposit collateral into the collateral pools, your collateral will be stored safely inside your Obligation object.

## Collateral Weight

To control the ratio of coins that can be borrowed out using a collateral coin, we need a parameter called **Collateral Weight** in each of the **Collateral Pools.** For example, if you deposited **1 BTC** to a **Collateral Pool** and the **BTC** price at the moment is $10,000. And the **Collateral Weight** of **the BTC Collateral Pool** is **70%**. That means you can only borrow out **70%** of your BTC coins value or equal to `$10,000 x 70% = $7,000` .

Collateral Weight usually has a value below 1.

How much you can borrow from the **assets pools** depends on your collateral values. Your collateral value is determined using this formula:

<figure><img src="../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Any changes regarding the **Collateral Weight** of a collateral pool that you deposited into will affect your **Collateral Value**.

## Borrow Weight

There are multiple coins that have a volatile price. One of the solutions to protecting users from volatile coins, we create a **borrow weight** feature so borrowing a volatile coin will be much “expensive”. The terms of expensive here mean you can only borrow less volatile coins with such collateral. Borrow weight will affect the amount of debt you have. This is how your debt is calculated:

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

For example, there are SUI and USDC assets pools.

USDC has a more stable price rather than SUI, hence we set the **Borrow Weight** to be **1** and **1.25** respectively. and then you deposited 1 BTC that is worth $10,000 to the **collateral pool** with **Collateral Weight** equal to **70%** and your collateral value is **$7,000** (70% of $10,000).

Let’s say the price of USDC is $1 and the price of SUI is also $1. With $7,000 you can borrow out 7,000 USDC **but** for SUI you can only borrow out 5,600 SUI.

## Zero Fee Flash Loans

A flash loan is a type of loan where a user borrows assets with no upfront collateral and returns the borrowed assets within the same blockchain transaction. Because Scallop only charges fees according to the time value of the coin, and from the blockchain's perspective flash loans are held for a duration of 0 seconds, they are entirely free on Scallop (ignoring Sui gas fee costs).
