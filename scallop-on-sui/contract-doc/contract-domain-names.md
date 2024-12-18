# Scallop contract domain names

Scallop embraces the vision of SuiNS to make it human readable for on-chain activity.

Each contract from scallop is assigned a subdomain name under `contracts@scallop`. This helps users to tell that they are interacting with a contract from Scallop, and also helps Scallop to manage the contracts.

## Naming convention

The naming convention is `<contract-name>_<major.minor.patch>.contracts@scallop`, or `<contract-name>.contracts@scallop` without version suffix.

For each contract, there could be multiple versions. The latest version is always the default one. For example, the latest version of `X-oracle` is `x-oracle.contracts@scallop`. For the old version, it is named as `x-oracle-v1.1.0.contracts@scallop`.

## Contract domain names

| Contract name                      | Contract address                                                 | description                             |
|------------------------------------|------------------------------------------------------------------|-----------------------------------------|
| market.contracts@scallop           | 0xb32236966eeb02ee85f8a49352f3dda0082433e94a0536ebe354ce911393f497 | Money market for lending and borrowing  |
| x-oracle.contracts@scallop         | 0x1478a432123e4b3d61878b629f2c692969fdb375644f1251cd278a4b1e7d7cd6 | X-oracle contract                       |
| sca.contracts@scallop              | 0x7016aae72cfc67f2fadf55769c0a7dd54291a583b63051a5ed71081cce836ac6 | Token contract of SCA                   |
| ve-sca.contracts@scallop           | 0x1158813b32962c2d22888fae257d5f2365b03631f0cd5d5b912ccdf51ff4e2f2 | VeSCA contract                          |
| loyalty-program.contracts@scallop  | 0xab7c4e6d53ef862a1115d0c381fd33e05f9c206b79f322a54990b1e8c2fe3446 | VeSCA loyalty program                   |
| referral-program.contracts@scallop | 0x1cd85ea1d3a9320a45312fab5649c97121f9d7f441a1ffcd026506c853442249 | Scallop referral program                |
| borrow-incentive.contracts@scallop | 0xd9f906db7f2fda2c22ca6320cb302f390939f16b5df60907f5237ce0b6d6eb56 | Borrow incentive contract               |
