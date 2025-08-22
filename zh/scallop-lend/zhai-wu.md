# 債務

在進行任何與借貸相關的活動之前，您必須擁有一個債務本`Obligation`。債務本是一個用於記錄您的抵押品和債務的物件。 因此，您需要至少創建一個債務本才能執行任何與借貸相關的操作。



{% hint style="info" %}
您可以擁有多個債務本



每個債務本都是獨立的，這意味著即使您是這些債務本的所有者，在一個債務本中存入抵押品並不能讓您使用另一個債務本來借貸資產。
{% endhint %}

## 深度了解債務物件

債務本`Obligation`是一個共享物件。債務本並非保存在您的錢包中，您擁有一個債務密鑰`ObligationKey`。這個債務密鑰作為您擁有特定債務物件的證明。因此，您在錢包中看到的是一個代表債務密鑰`ObligationKey`的 NFT。

基本上，您的債務本可以包含在任何交易中。然而，對於某些需要所有權證明的操作，其他人無法使用您的債務本，因為這些操作需要所有權的證明。這時，您的債務密鑰發揮了關鍵作用。

例如，當您想要借款時，借款功能將要求您提供債務本`Obligation`和債務密鑰`ObligationKey`。在這種情況下，任何人都可以在這個功能中傳遞您的債務本`Obligation`，但只有您可以使用正確的債務密鑰`ObligationKey`。這一機制保障了您的債務本不被未經授權使用。

這正是我們從 Sui 以物件中心的模型中獲得之優勢。[https://docs.sui.io/concepts/object-ownership/address-owned](https://docs.sui.io/concepts/object-ownership/address-owned)

