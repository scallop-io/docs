# Risks & Auditing

## Risks of using Scallop

All DeFi protocols, including Scallop, come with risks, which are important to understand before depositing significant amounts of crypto. The main risks involved in using Scallop are outlined here.

**Smart Contract Risk**

This is a risk that the Scallop smart contracts get exploited to steal or permanently freeze funds. This risk is inherent to all smart contracts and can never be fully eliminated, but can be mitigated in various ways.

**Oracle Risk**

Scallop relies on Pyth, Switchboard, and Supra Oracles for their price feeds. Although we have an [Aggregate Multi-Oracle Strategy](oracles.md#aggregate-multi-oracle-strategy) to avoid one single oracle getting attacked and let us get the incorrect price feed. There is still a risk that these oracles report incorrect prices at the same time, causing wrongful liquidation.

#### Wallet Providers **Risk**

Scallop is compatible with a wide range of wallets, including Martian, Suiet, Elli, Ethos Waller, and an open-source Sui wallet called Sui Wallet, any Sui wallet exploit could affect some of the Scallop users.

## Insurance Fund

The Insurance Fund reserve ensures protection for unforeseen losses caused by untimely liquidations within insured pools. Additionally, it safeguards against incorrect price feeds and manipulation issues arising from oracles.

It is crucial to bear in mind that Scallop Insurance Fund payouts are reserved for highly volatile market conditions or instances of oracle failure. Nonetheless, it remains essential for users to exercise due diligence when evaluating the oracles employed or parameters established for each pool. Compensation for minor oversights resulting from a lack of due diligence will not be entertained.

## Borrow/Outflow/Collateralization Rate Limits

Scallop implements a dynamic constraint on the total sum of loans and withdrawals permitted, which can be adjusted for each asset and pool. As an illustration, a limit of $1M may be set for borrowing or withdrawing from the primary pool within a single 24-hour timeframe.

## Is Scallop Sui smart contract audited/open-source?

The Scallop auditing process is ongoing by [MoveBit](https://www.movebit.xyz/) & [OtterSec](https://osec.io/), we will publish the auditing report after it is finished and make Scallop V1 an open-sourced protocol on the Sui blockchain.
