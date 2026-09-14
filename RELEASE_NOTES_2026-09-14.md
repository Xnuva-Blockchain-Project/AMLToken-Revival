# AMLToken Revival — Public Technical Preview

**Release date:** 14 September 2026

## What this release is

This is the first public technical/evidence preview of the independent AMLToken Revival project.

The purpose of this release is to make the reconstruction work visible, document what the preserved original software proves, and attract holders/researchers who may still possess historical AMLToken blockchain data.

This is **not** a live production-chain release, not a new token launch, and not a balance-migration event.

## Verified at this checkpoint

The project has established and documented:

- preserved original AMLToken-Qt v1.3.0 Windows and Linux artefacts and hashes;
- exact recovery/reproduction of the original AMLToken mainnet genesis;
- recovered mainnet network identity and key consensus parameters;
- Bitcoin-style SHA256d proof of work;
- historical wallet-format compatibility with the preserved original client;
- a historical `PeerAllowed()` authorization mechanism tied to a 13-entry authorized-peer table;
- five direct `PeerAllowed()` call sites covering outbound connection progression, eviction/retention, address handling, block handling and compact-block handling;
- an evidence-backed revival policy that removes the historical peer-authorization dependency without changing genesis, historical ownership or consensus validity;
- a successful isolated two-node protocol-70015 ordinary-peer handshake at height 0 with no replacement blocks mined.

## Why the peer-control evidence matters

The preserved original binary shows that AMLToken used an operator-defined authorized-peer list as an active control in the normal outbound connection path, with additional uses in later peer/message-processing logic.

That mechanism is preserved as historical evidence but is not reproduced as an authorization authority in the revival.

The technical record is published in:

- `docs/HISTORICAL_NETWORK_CONTROL_EVIDENCE.md`
- `docs/NETWORK_REVIVAL_POLICY.md`

## What is still missing

The legitimate post-genesis AMLToken/ABTC blockchain has not yet been recovered.

Without that history, the project will **not**:

- mine a new production history from genesis;
- manufacture balances;
- rewrite transactions;
- claim wallet-local records are independently chain-confirmed;
- present a reconstructed replacement ledger as the original chain.

## Call for historical data

Anyone who ran AMLToken in the original period may have useful chain evidence on an old PC, drive, backup or server image.

Potentially useful non-private material includes:

- historical `.amltoken` data directories;
- `blocks/` and `blk*.dat` files;
- chainstate data;
- old public installers/packages;
- archived source code;
- historical block-explorer records;
- public block hashes, transaction IDs or node information.

**Do not publish or upload wallet files, private keys, seed phrases or passphrases.**

## Project pause

The active reconstruction work is expected to pause for approximately six weeks after this preview. The repository contains a dated project checkpoint so work can resume without relying on undocumented state.

During the pause, the most valuable contribution is locating preserved historical blockchain evidence.

## Guiding rule

**Same genesis. Same historical ledger. Same ownership.**

The goal is recovery, not replacement.
