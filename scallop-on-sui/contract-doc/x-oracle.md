# Core Scallop Contract - X-oracle
X-oracle aggregates price feeds from multiple oracle providers, and output a price feed if the consensys is meet among these oracle providers.
Adapter pattern is adpoted to allow different oracles to work together.

### Contract design

high level graphic representation of contract design
![Contract design](graphic/Xoracle-design.png)

**Description:**

X-oracle aggregates price feeds from different oracle providers. One of the provider is set as the main source.
Other price feeds are compared to the main price feed, if majority of price feeds is within a specific range to the main source,
then the price update is successful, otherwise will reject the update.
For example, there're 5 oracle providers. If 2 out of the 4 non-major price feeds is within the range compared to main price feeds,
then the update is good. Less than 2 is within range, then update is bad.

Currently
- the valid price range is 99% ~ 101% compared to main price feed.
- main oracle provider is Pyth, and only 1 oracle provider is supported current.


## Contract Source & Deployment

### X-oracle

https://github.com/scallop-io/sui-lending-protocol/tree/main/contracts/sui_x_oracle/x_oracle

**Initial package**: 0x1478a432123e4b3d61878b629f2c692969fdb375644f1251cd278a4b1e7d7cd6

**Latest package**: 0x1478a432123e4b3d61878b629f2c692969fdb375644f1251cd278a4b1e7d7cd6

### Pyth adaptor

https://github.com/scallop-io/sui-lending-protocol/tree/main/contracts/sui_x_oracle/pyth_rule

**Initial package**: 0x910f30cbc7f601f75a5141a01265cd47c62d468707c5e1aecb32a18f448cb25a

**Latest package**: 0x910f30cbc7f601f75a5141a01265cd47c62d468707c5e1aecb32a18f448cb25a


(Notice: Supra adaptor, Switchboard adpator is not deployed in production yet due to price feed incomplete yet)


