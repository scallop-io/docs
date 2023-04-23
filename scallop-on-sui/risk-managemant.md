# Risk Managemant

### Protected Collateral Vault

`//TODO`

### Collateral Weights

| Pool | Asset | Collateral Weights |
| ---- | ----- | ------------------ |
| Main | wBTC  | 80%                |
| Main | wETH  | 70%                |
| Main | SUI   | 60%                |
| Main | USDC  | 90%                |
| Main | USDT  | 90%                |

### Insurance Fund

`//TODO`

### Borrow/Outflow/Collateralization Rate Limits

Scallop implements a dynamic constraint on the total sum of loans and withdrawals permitted, which can be adjusted for each asset and pool. As an illustration, a limit of $1M may be set for borrowing or withdrawing from the primary pool within a single 24-hour timeframe.

