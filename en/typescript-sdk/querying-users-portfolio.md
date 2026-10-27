# Querying User's Portfolio

The portfolio gives a complete view of a wallet's positions in Scallop: supplied assets, staked assets, collaterals, borrowings and locked veSCA. **`ScallopQuery`** can read it with a single call.

```typescript
import { ScallopQuery } from '@scallop-io/sui-scallop-sdk';

const scallopQuery = new ScallopQuery({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  walletAddress: '0x...',
});

await scallopQuery.init();
```

## Get User Portfolio

```typescript
const portfolio = await scallopQuery.getUserPortfolio();

// Or for another wallet
const other = await scallopQuery.getUserPortfolio({ walletAddress: '0x...' });
```

The portfolio combines the lending, obligation account and veSCA data of the wallet, including total values (USD) and totals across all positions.

## Get Lending Positions

To read only the lending side, use `getLendings`. It returns the supplied and staked amounts, the supply APY and the amounts available to supply, withdraw, stake, unstake and claim.

```typescript
// All whitelisted pools
const lendings = await scallopQuery.getLendings();

// Specific pools
const { sui, usdc } = await scallopQuery.getLendings(['sui', 'usdc']);
console.log(sui?.suppliedCoin); // supplied amount in coin unit
console.log(sui?.suppliedValue); // supplied value in USD
console.log(sui?.supplyApy);
console.log(sui?.availableWithdrawCoin);

// Single pool
const lending = await scallopQuery.getLending('sui');
```

## Get Borrowing Positions

Borrowing positions are part of the obligation accounts. See [Querying Obligation Accounts](querying-obligation-accounts.md).

```typescript
const obligationAccounts = await scallopQuery.getObligationAccounts();
```

## Get Wallet Balances

```typescript
// Underlying coins, keyed by coin name
const coinAmounts = await scallopQuery.getCoinAmounts(['sui', 'usdc']);

// sCoins (e.g. sSUI), keyed by the sCoin's market coin name
const sCoinAmounts = await scallopQuery.getSCoinAmounts();

// Old market coins, for users that have not migrated to sCoin
const marketCoinAmounts = await scallopQuery.getMarketCoinAmounts();
```

## Get veSCA

```typescript
// All veSCA keys owned by the wallet, excluding empty ones
const veScas = await scallopQuery.getVeScas({ excludeEmpty: true });
```

## Migrate Market Coins to sCoins

Users who still hold old market coins (and staked market coins in spool) can convert all of them into sCoins in one transaction. This is a write action, so it uses `ScallopClient`.

```typescript
import { ScallopClient } from '@scallop-io/sui-scallop-sdk';

const scallopClient = new ScallopClient({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  secretKey: '...', // or mnemonics: '...'
});

await scallopClient.init();

const { effects, digest } = await scallopClient.migrateAllMarketCoin();
console.log(`${effects?.status.status}: ${digest}`);
```
