# Risks

## Risks of using Scallop

All DeFi protocols, including Scallop, come with risks, which are important to understand before depositing significant amounts of crypto. The main risks involved in using Scallop are outlined here.

**Smart Contract Risk**

This is a risk that the Scallop smart contracts get exploited to steal or permanently freeze funds. This risk is inherent to all smart contracts and can never be fully eliminated, but can be mitigated in various ways.

**Oracle Risk**

Scallop relies on Pyth, Switchboard, and Supra Oracles for their price feeds. Although we have an [Aggregate Multi-Oracle Strategy](oracles.md#aggregate-multi-oracle-strategy) to avoid one single oracle getting attacked and let us get the incorrect price feed. There is still a risk that these oracles report incorrect prices at the same time, causing wrongful liquidation.

#### Wallet Providers **Risk**

Scallop is compatible with a wide range of wallets, including Martian, Suiet, Elli, Ethos Waller, and an open-source Sui wallet called Sui Wallet, any Sui wallet exploit could affect some of the Scallop users.

#### Regulatory risk

The regulatory status of Scallop, $SCA, and distributed ledger technology is unclear or unsettled in many jurisdictions. The regulation of digital assets has become a primary target of regulation in all major countries in the world. It is impossible to predict how, when, or whether regulatory agencies may apply existing regulations or create new regulations with respect to such technology and its applications, including $SCA and/or Scallop. Regulatory actions could negatively impact $SCA and/or Scallop in various ways. The Company, the Distributor (or their respective affiliates) may cease operations in a jurisdiction in the event that regulatory actions, or changes to law or regulation, make it illegal to operate in such jurisdiction, or commercially undesirable to obtain the necessary regulatory approval(s) to operate in such jurisdiction. After consulting with a wide range of legal advisors to mitigate the legal risks as much as possible, the Company and Distributor have worked with the specialist blockchain department at Jacque Law LLC and obtained a legal opinion on the token distribution, and will be conducting business in accordance with the prevailing market practice.

#### Risk of insufficient information

As of the date hereof, Scallop is still under development and its design concepts, consensus mechanisms, algorithms, codes, and other technical details and parameters may be constantly and frequently updated and changed. Although this material contains the most current information relating to Scallop, it is not absolutely complete and may still be adjusted and updated by the Scallop Project Contributors from time to time. The Scallop Project Contributors have neither the ability nor obligation to keep holders of $SCA informed of every detail (including development progress and expected milestones) regarding the project to develop Scallop, hence insufficient information disclosure is inevitable and reasonable.

#### Competitive Risk

Various types of decentralized applications, games, and networks are emerging at a rapid rate, and the industry is increasingly competitive. It is possible that alternative networks could be established that utilize the same or similar code and protocol underlying $SCA and/or Scallop and attempt to re-create similar facilities. Scallop may be required to compete with these alternative networks, which could negatively impact $SCA and/or Scallop.

#### Risk of failure to develop

There is the risk that the development of Scallop will not be executed or implemented as planned, for a variety of reasons, including without limitation the event of a decline in the prices of any digital asset, virtual currency, or $SCA, unforeseen technical difficulties, and shortage of development funds for activities.

## Insurance Fund

The Insurance Fund reserve ensures protection for unforeseen losses caused by untimely liquidations within insured pools. Additionally, it safeguards against incorrect price feeds and manipulation issues arising from oracles.

It is crucial to bear in mind that Scallop Insurance Fund payouts are reserved for highly volatile market conditions or instances of oracle failure. Nonetheless, it remains essential for users to exercise due diligence when evaluating the oracles employed or parameters established for each pool. Compensation for minor oversights resulting from a lack of due diligence will not be entertained.

## Borrow/Outflow/Collateralization Rate Limits

Scallop implements a dynamic constraint on the total sum of loans and withdrawals permitted, which can be adjusted for each asset and pool. As an illustration, a limit of $1M may be set for borrowing or withdrawing from the primary pool within a single 24-hour timeframe.
