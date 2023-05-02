# Oracles

_`Due to the inconsistent launch times of third-party Oracle services on the Sui mainnet, we will initially only use the Switchboard. Subsequently, we will upgrade and introduce more reliable on-chain price feeds.`_

The components of the Scallop price modules planning include Supra Oracles, Switchboard, and Pyth. These price feeds are essential for assessing account health and determining liquidation. Each Oracle operates with a refresh rate based on their feeds, and we use their **TWAP Oracles** for a better security level, which can be further explored at the following links.

* **Supra Oracles**: [https://data.supraoracles.com/networks](https://data.supraoracles.com/networks)
* **Switchboard**: [https://switchboard.xyz/explorer](https://switchboard.xyz/explorer)
* **Pyth**: [https://pyth.network/price-feeds](https://pyth.network/price-feeds)

What are **TWAP Oracles?** \
[https://www.halborn.com/blog/post/what-are-twap-oracles](https://www.halborn.com/blog/post/what-are-twap-oracles)

#### Aggregate Multi-Oracle Strategy

To reduce the risk of price manipulation in lending protocols, we use multiple oracles and evaluate their published prices. If any anomalies are detected, we abort the operation. A primary oracle is chosen as the main data source, while additional oracles serve as supplementary proof for the primary oracle's price.
