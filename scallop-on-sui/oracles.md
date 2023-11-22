# Oracles

## Multi-Oracle

The components of the Scallop price modules planning include **Pyth, Switchboard**, and **Supra Oracles**. These price feeds are essential for assessing account health and determining liquidation. Each Oracle operates with a refresh rate based on their feeds, and we use their **TWAP Oracles** for a better security level, which can be further explored at the following links.

* **Pyth**: [https://pyth.network/price-feeds](https://pyth.network/price-feeds)
* **Switchboard**: [https://switchboard.xyz/explorer](https://switchboard.xyz/explorer)
* **Supra Oracles**: [https://data.supraoracles.com/networks](https://data.supraoracles.com/networks)

## Aggregate Multi-Oracle Strategy

To reduce the risk of price manipulation in lending protocols, we have added an extra layer of security for the oracle (the oracle responsible for price provider), we use multiple oracles and evaluate their published prices. If any anomalies are detected, we abort the operation. A primary oracle is chosen as the main data source, while additional oracles serve as supplementary proof for the primary oracle's price.

## **\*TWAP Oracles (Building)**

Blockchain oracles supply real-world data to smart contracts in DeFi, such as asset prices or election outcomes. To protect DeFi smart contracts from price manipulation, Time Weighted Average Price (TWAP) oracles have been implemented to improve security.

A TWAP oracle provides the average price of an asset over a specific period, making price manipulation costly and difficult for attackers. TWAP oracles calculate asset prices using weighted averages, with time serving as the weight. This method is more accurate than a simple average, as it assigns significance to certain values in a distribution.

TWAP oracles, introduced in Uniswap v2 and improved in Uniswap v3, offer a more secure alternative to spot price or off-chain oracles. They are less susceptible to collusion and more resilient to short-term price fluctuations and flash loans. Thus, TWAP oracles are crucial for DeFi security.
