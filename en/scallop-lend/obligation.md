# Obligation

Before engaging in any borrowing-related activities, you must have an `Obligation` object. An `Obligation` is an object used to record your collateral and debt. Therefore, you need to create at least one `Obligation` to perform any actions related to borrowing.



{% hint style="info" %}
It’s possible to have multiple obligations.



Each obligation is independent of the others, meaning that depositing collateral in one obligation does not allow you to borrow an asset using another obligation—even if you are the owner of both obligations.
{% endhint %}

## Understanding Obligation in deep



An `Obligation` is a shared object. instead of holding the `Obligation` object in your wallet, you will possess an `ObligationKey`. This `ObligationKey` serves as proof that you own a specific `Obligation` linked to this **key**. Consequently, what you will find in your wallet is an NFT of the `ObligationKey`.



Essentially, your `Obligation` can be included in any transaction. However, for certain actions that _require proof of ownership_, others cannot use your `Obligation` because the function requires ownership proof. This is where your `ObligationKey` **plays a crucial role**. \


For instance, when you want to borrow, the borrowing function will require you to provide both the `Obligation` and `ObligationKey` objects. In this scenario, anyone could pass your `Obligation` in this function, BUT **only you** can use the **correct** `ObligationKey`. This mechanism secures your `Obligation` against unauthorized use.

\
This is what we leverage from Sui Object-centric Model [https://docs.sui.io/concepts/object-ownership/address-owned](https://docs.sui.io/concepts/object-ownership/address-owned)

