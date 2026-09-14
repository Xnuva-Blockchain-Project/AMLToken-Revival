# AMLToken Revival — Public Technical Preview

**Release date:** 14 September 2026  
**Updated:** 14 September 2026 following historical-chain recovery, redundant public-node deployment and publication of the independent-reproduction framework

## What this release is

This is the first public technical/evidence preview of the independent AMLToken Revival project.

The purpose of this release is to make the reconstruction work visible, document what the preserved original software proves, preserve recovered historical chain evidence, and attract holders/researchers who may still possess later AMLToken blockchain data.

This is **not** a live replacement-chain launch, not a new token launch, and not a balance-migration event.

## Verified at this checkpoint

The project has established and documented:

- preserved original AMLToken-Qt v1.3.0 Windows and Linux artefacts and hashes;
- exact recovery/reproduction of the original AMLToken mainnet genesis;
- recovered mainnet network identity and key consensus parameters;
- Bitcoin-style SHA256d proof of work;
- historical wallet-format compatibility with the preserved original client;
- recovered original AMLToken monetary and coinbase-maturity rules from preserved binary evidence;
- an authenticated historical raw block stream from genesis through height **175168**;
- fresh end-to-end reindex validation of that snapshot on three separate project-controlled machines;
- exact reproduction of the same historical tip and chainwork on all three systems;
- a historical `PeerAllowed()` authorization mechanism tied to a 13-entry authorized-peer table;
- five direct `PeerAllowed()` call sites covering outbound connection progression, eviction/retention, address handling, block handling and compact-block handling;
- an evidence-backed revival policy that removes the historical peer-authorization dependency without changing genesis, historical ownership or consensus validity;
- two public walletless, non-mining archival/discovery nodes on separate networks serving the validated snapshot;
- a public independent-reproduction standard that explicitly distinguishes project-controlled validation from true third-party replication.

## Historical chain recovery update

An authenticated AMLToken blockchain snapshot has now been recovered and validated through:

```text
height: 175168
bestblockhash: 000000008be329b7f5186e61c86367ece62db781374cc7c4fee46ba296b40025
genesis: 00000000230d6b389555e80e4523a32343531448ddd15fbc29c0fdc11dbb1538
chainwork: 00000000000000000000000000000000000000000000000000048f2b9dfa1d51
```

The preserved raw block file used for validation has SHA256:

```text
77b005775f3d87429571a52b491aeadd0787b3350b3b96249fb1a169964cbf03
```

Fresh reindexes on three separate project-controlled machines reached the same height, tip and chainwork without consensus rejection.

See `docs/HISTORICAL_CHAIN_RECOVERY.md` for the technical recovery record.

## Independent reproduction milestone

The project does not treat three project-operated machines as equivalent to independent third-party replication.

The target standard is:

**Do not trust our result. Reproduce it.**

A complete outsider replay from GitHub alone is not yet possible because two public artefacts still have to be published in durable form:

- the exact clean reconstruction source tree corresponding to commit `8b821d120b6331cb9ac83c764863e032f567b776`;
- the preserved public historical `blk00000.dat` with SHA-256 `77b005775f3d87429571a52b491aeadd0787b3350b3b96249fb1a169964cbf03`.

The expected outputs, verification procedure and reporting standard are published in `docs/INDEPENDENT_REPRODUCTION.md`.

Completion of the self-contained public package and the first unaffiliated reproduction are tracked in GitHub Issue #3.

Until that happens, the project will describe the current result as **project-controlled multi-host reproduction**, not independent third-party reproduction.

## Public archival/discovery nodes

The validated snapshot is now served by two walletless, non-mining public nodes on separate networks:

```text
Primary (T620):        81.130.208.151:23247
Secondary (Contabo):  84.247.164.62:23247
```

Both endpoints have been externally verified as reachable from the other network.

Separate canonical snapshots are preserved independently from the live working datadirs so later P2P activity cannot alter the archival baseline.

The nodes are independent recovery endpoints. Candidate later history received by either node must still be preserved and independently validated before it is accepted as authenticated history.

## Why the peer-control evidence matters

The preserved original binary shows that AMLToken used an operator-defined authorized-peer list as an active control in the normal outbound connection path, with additional uses in later peer/message-processing logic.

That mechanism is preserved as historical evidence but is not reproduced as an authorization authority in the revival.

The technical record is published in:

- `docs/HISTORICAL_NETWORK_CONTROL_EVIDENCE.md`
- `docs/NETWORK_REVIVAL_POLICY.md`

## What is still missing

Block **175168 is the latest authenticated snapshot currently recovered**. It is not being claimed as the final historical AMLToken network tip.

The main remaining recovery target is therefore historical data **later than height 175168**.

The main remaining reproducibility target is publication of the exact clean reconstruction source tree and preserved public historical raw block file so an unaffiliated reviewer can replay the recovery without trusting project-operated machines.

The project will not:

- mine a replacement production history from the recovered snapshot merely to create activity;
- manufacture balances;
- rewrite transactions;
- treat a longer peer-supplied continuation as authentic without independent validation;
- present reconstructed or synthetic ledger data as original history;
- claim independent third-party reproduction before an unaffiliated reviewer has actually reproduced the public result.

## Call for later historical data

Anyone who ran AMLToken in the original period may have useful chain evidence on an old PC, drive, backup, exchange node, pool server or VPS image.

Potentially useful non-private material includes:

- historical `.amltoken` data directories;
- `blocks/` and `blk*.dat` files, especially data extending beyond height 175168;
- later chainstate or block-index data;
- old public installers/packages;
- archived source code;
- historical block-explorer records;
- later public block height/hash pairs;
- transaction IDs or archived node information.

**Do not publish or upload wallet files, private keys, seed phrases or passphrases.**

## Guiding rule

**Same genesis. Same historical ledger. Same ownership.**

The goal is recovery and preservation, not replacement.
