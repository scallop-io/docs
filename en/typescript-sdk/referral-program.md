# Referral Program

The referral program lets a **veSCA** holder earn a share of the borrow fees paid by the users that are **bound** to their veSCA. A user binds to one referrer; the referrer then claims the accumulated revenue.

## Bind to a Referrer

A user binds to a referrer by using the referrer's veSCA key id. Borrowing after the binding pays part of the borrow fee to the referrer.

```typescript
import { ScallopBuilder } from '@scallop-io/sui-scallop-sdk';

const scallopBuilder = new ScallopBuilder({
  addressId: '695fcdc084f790c04eb068dc',
  fullnodeUrl: 'https://fullnode.mainnet.sui.io:443',
  secretKey: '...', // or mnemonics: '...'
});

await scallopBuilder.init();

const tx = scallopBuilder.createTxBlock();
tx.setSender(scallopBuilder.walletAddress);

tx.bindToReferral('0x...referrerVeScaKeyId');

const { effects, digest } = await scallopBuilder.signAndSendTxBlock(tx);
console.log(`${effects?.status.status}: ${digest}`);
```

## Check Referral Binding

Returns the veSCA key id of the referrer that the wallet is bound to, or `null` if there is none.

```typescript
const referrerVeScaKey =
  await scallopBuilder.query.getVeScaKeyIdFromReferralBindings();

// Check another wallet
const other = await scallopBuilder.query.getVeScaKeyIdFromReferralBindings('0x...');
```

## Unbind from a Referrer

```typescript
const tx = scallopBuilder.createTxBlock();
tx.setSender(scallopBuilder.walletAddress);

tx.unbindReferral();

const { effects, digest } = await scallopBuilder.signAndSendTxBlock(tx);
console.log(`${effects?.status.status}: ${digest}`);
```

## Claim Referral Revenue

The referrer claims the revenue with their veSCA key. `claimReferralRevenueQuick` claims the revenue of every given pool and sends it to the sender.

```typescript
const tx = scallopBuilder.createTxBlock();
tx.setSender(scallopBuilder.walletAddress);

// Claim the revenue of specific pools. Defaults to all pools if omitted
await tx.claimReferralRevenueQuick('0x...veScaKeyId', ['sui', 'usdc']);

const { effects, digest } = await scallopBuilder.signAndSendTxBlock(tx);
console.log(`${effects?.status.status}: ${digest}`);
```
