# Historical Chain Recovery

> Status: validated 14 September 2026

The AMLToken Revival project has recovered an authenticated historical AMLToken/ABTC blockchain snapshot and independently validated it from the original mainnet genesis through block **175168**.

This is a recovery of historical chain data. It is **not** a replacement chain, a new genesis, a balance recreation, or a synthetic migration.

## Validated snapshot identity

```text
height: 175168
bestblockhash: 000000008be329b7f5186e61c86367ece62db781374cc7c4fee46ba296b40025
genesis: 00000000230d6b389555e80e4523a32343531448ddd15fbc29c0fdc11dbb1538
```

The preserved historical raw block file used for validation has SHA256:

```text
77b005775f3d87429571a52b491aeadd0787b3350b3b96249fb1a169964cbf03
```

The recovered raw block stream contains 175169 block records, beginning with the authentic AMLToken genesis and extending through height 175168.

## Consensus reconstruction required for validation

The initial reconstruction inherited Bitcoin monetary and coinbase-maturity rules that did not match the preserved AMLToken chain. The original AMLToken-Qt v1.3.0 binary was therefore used as primary evidence to recover the historical rules rather than weakening validation or inventing exceptions.

Recovered rules include:

- `MAX_MONEY = 200,000,000 * COIN`;
- a special height-1 subsidy/allocation of `145,000,000 * COIN`;
- the original non-height-1 subsidy behaviour of 100 base units while the subsidy-interval quotient is at most 63, then zero;
- `COINBASE_MATURITY = 20` blocks.

After those evidence-derived rules were restored, a fresh reindex accepted the recovered chain from genesis through height 175168 without consensus rejection.

## Independent validation

The complete snapshot was independently reindexed on two separate machines using the same clean reconstruction build.

Both validations independently reproduced:

```text
blocks:  175168
headers: 175168
bestblockhash: 000000008be329b7f5186e61c86367ece62db781374cc7c4fee46ba296b40025
```

The historical raw block file remained byte-for-byte unchanged during validation.

## Public archival/discovery node

A walletless, non-mining public node now serves the validated snapshot at:

```text
81.130.208.151:23247
```

Compatible historical AMLToken nodes may connect with:

```text
addnode=81.130.208.151:23247
```

The endpoint has been externally verified as reachable from an independent Internet host.

The live node uses a working copy. A separate canonical validated snapshot is preserved so later peer activity cannot alter the archival evidence.

## Important boundary

Block **175168 is the latest authenticated snapshot currently recovered**. It is **not** being claimed as the final historical AMLToken network tip.

Historical data extending beyond height 175168 remains especially valuable. Any later blocks supplied by a peer or recovered from another archive must independently satisfy chain continuity and consensus validation before being treated as authenticated history.

## Holder safety

The recovery project does not need private wallet material. Do **not** publish or send:

- `wallet.dat`;
- private keys;
- seed phrases;
- wallet passphrases;
- `dumpwallet` output;
- `dumpprivkey` output.

Useful evidence includes non-private `blk*.dat` files, `blocks/` directories, block-index data, block height/hash pairs, historical public binaries, old source archives, explorer exports and archived node information.

## Preservation rule

**Same genesis. Same historical ledger. Same ownership.**

Recovered history is validated and preserved. It is not rewritten.
