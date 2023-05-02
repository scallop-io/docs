# Transferable Portfolio

Being a lender means depositing to the **assets pools**, depositing to the asset pool will give you Market Coins in return. Market Coins are transferable coins. You can transfer one, some, or all of it to anyone.

Borrowers also have the same privilege, they can transfer their Portfolio. In Scallop, we calculate your collateral and your debt inside an object called `Obligation`. To mutate this object you will need an object called `Obligation Key`, each `Obligation Key` belongs to an `Obligation` object. So when you create an `Obligation` object for the first time, you will get `Obligation Key` in return and it will be stored inside your address. This `Obligation Key` is just like an NFT, it represents ownership and it’s transferable. Transferring your `Obligation Key` to the other address means you hand over your ownership to someone else.
