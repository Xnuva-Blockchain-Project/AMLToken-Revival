# Historical Chain Recovery

> Status: validated 14 September 2026

The AMLToken Revival project has recovered an authenticated historical AMLToken/ABTC blockchain snapshot and validated it from the original mainnet genesis through block **175168**.

This is a recovery of historical chain data. It is **not** a replacement chain, a new genesis, a balance recreation, or a synthetic migration.

Because the ticker **ABTC** is also used by unrelated modern projects, readers should also see [`ABTC_IDENTITY_AND_CONTEXT.md`](ABTC_IDENTITY_AND_CONTEXT.md) for the distinction between the native historical AMLToken chain, unrelated contract tokens, current market claims and the legal history of the former AML Bitcoin project.

## Validated snapshot identity

```text
height: 175168
bestblockhash: 000000008be329b7f5186e61c86367ece62db781374cc7c4fee46ba296b40025
genesis: 00000000230d6b389555e80e4523a32343531448ddd15fbc29c0fdc11dbb1538
chainwork: 00000000000000000000000000000000000000000000000000048f2b9dfa1d51
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

## Multi-host project validation

The complete snapshot was freshly reindexed on **three separate project-controlled machines** using the same clean reconstruction build:

- the reconstruction/development host;
- the T620 archival node host;
- the Contabo secondary archival node host.

All three validations independently reproduced:

```text
blocks:  175168
headers: 175168
bestblockhash: 000000008be329b7f5186e61c86367ece62db781374cc7c4fee46ba296b40025
chainwork: 00000000000000000000000000000000000000000000000000048f2b9dfa1d51
```

The historical raw block file remained byte-for-byte unchanged during validation.

These runs are strong cross-machine validation, but all three machines were operated by the project. They are therefore **not being represented as independent third-party reproduction**.

## Independent reproduction status

The project now has an explicit public reproducibility standard: **do not trust our result; reproduce it**.

A complete outsider replay from GitHub alone is not yet possible because two artefacts still need to be published in durable public form:

- the exact clean reconstruction source tree corresponding to commit `8b821d120b6331cb9ac83c764863e032f567b776`;
- the preserved public historical `blk00000.dat` with SHA-256 `77b005775f3d87429571a52b491aeadd0787b3350b3b96249fb1a169964cbf03`.

The expected outputs, verifier procedure and reporting standard are documented in [`INDEPENDENT_REPRODUCTION.md`](INDEPENDENT_REPRODUCTION.md). Completion of the public package and the first unaffiliated reproduction are tracked in [GitHub Issue #3](https://github.com/Xnuva-Blockchain-Project/AMLToken-Revival/issues/3).

The project will not claim independent third-party reproduction until an unaffiliated reviewer has completed the public procedure on their own system.

## Public archival/discovery nodes

Two walletless, non-mining public nodes now serve the validated snapshot on separate networks:

```text
Primary (T620):        81.130.208.151:23247
Secondary (Contabo):  84.247.164.62:23247
```

Compatible historical AMLToken nodes may connect with:

```text
addnode=81.130.208.151:23247
addnode=84.247.164.62:23247
```

Both endpoints have been externally verified as reachable from the other network.

Each public node uses a working copy. Separate canonical validated snapshots are preserved so later peer activity cannot alter the archival evidence.

The public nodes are independent recovery endpoints rather than authorities for one another. Later data received by either node remains candidate continuation evidence until separately preserved and validated.

Old wallet holders who need non-technical connection instructions should use the **[Old AMLToken / ABTC Wallet — Simple Connection Guide](OLD_WALLET_CONNECTION_GUIDE.md)** before changing anything in their historical installation.

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

For old-wallet backup, data-folder and connection instructions, see [`OLD_WALLET_CONNECTION_GUIDE.md`](OLD_WALLET_CONNECTION_GUIDE.md).

For legal-history, ticker and chain-identity clarification, see [`ABTC_IDENTITY_AND_CONTEXT.md`](ABTC_IDENTITY_AND_CONTEXT.md).

## Preservation rule

**Same genesis. Same historical ledger. Same ownership.**

Recovered history is validated and preserved. It is not rewritten.
