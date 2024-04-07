# Core Scallop Contract
Scallop is a decentralized money market on SUI, designed for the efficient lending/borrowing assets.

This documentation outlines the technical implementation of the core Scallop protocol and related smart contracts.
It may be useful for third-party integrators, or technically proficient users of the protocol.

## Structure
Core smart contracts include
- Scallop protocol
- X-oracle
- General libraries

### [Scallop protocol](./scallop-protocol.md)
This part contains all the business logic related to the lending/borrowing, such as mint/redeem of sCoin, calculation of debts, liquidation. 


### [X-oracle](./x-oracle.md)
Scallop uses X-oracle to fetch asset prices. It contains a multi-oracle strategy, and several adaptors for different oracles such as Pyth, Supra, Switchboard.

### [General libraries](./general-libraries.md)
The libraries contains coin decimal utils, math lib, whitelist utils, enhanced move structures.



