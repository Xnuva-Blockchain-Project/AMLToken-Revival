# Public Historical-Chain Archival/Discovery Node

> Status: active as of 14 September 2026

A public AMLToken/ABTC archival and recovery node is available at:

```text
81.130.208.151:23247
```

## Purpose

This node serves the latest authenticated historical AMLToken/ABTC snapshot currently recovered and remains available to compatible historical nodes that may possess later chain data.

It is **not** a replacement production chain, a new token launch, or a mining endpoint.

The node is deliberately operated:

- without a wallet;
- without mining;
- with the recovered original AMLToken mainnet genesis;
- with the independently validated historical snapshot through height 175168;
- with ordinary peer connectivity rather than the historical operator-controlled authorization gate;
- with no invented blocks, balances or ownership changes.

## Current authenticated chain state

```text
blocks:  175168
headers: 175168
bestblockhash: 000000008be329b7f5186e61c86367ece62db781374cc7c4fee46ba296b40025
genesis: 00000000230d6b389555e80e4523a32343531448ddd15fbc29c0fdc11dbb1538
```

The raw historical block file used to reconstruct and validate this snapshot has SHA256:

```text
77b005775f3d87429571a52b491aeadd0787b3350b3b96249fb1a169964cbf03
```

Fresh full reindexes on two separate machines independently reproduced the same height, tip and genesis without consensus rejection.

Block **175168 is the latest authenticated snapshot currently recovered**. It is **not** being claimed as the final historical AMLToken network tip.

## Connecting a surviving historical node

If you operate a surviving AMLToken node containing historical chain data, especially data later than height 175168, you may point it at the recovery endpoint using an ordinary addnode entry:

```text
addnode=81.130.208.151:23247
```

The public service accepts compatible inbound P2P connections. It is not configured to actively roam for arbitrary peers.

Please preserve your existing data directory before making changes. Work from a copy where possible.

Any later headers or blocks supplied by a peer must still pass normal chain-continuity and consensus validation before they can be treated as authenticated historical ledger data.

## Archival separation

The public node runs from a working copy of the validated chain state.

A separate canonical snapshot of the validated height-175168 baseline is preserved independently. This keeps later P2P activity separate from the archival evidence used to establish the recovered historical baseline.

## Wallet and private-key safety

Do **not** publish or send:

- `wallet.dat`;
- private keys;
- seed phrases;
- wallet passphrases;
- `dumpwallet` or `dumpprivkey` output.

The recovery effort needs public blockchain history, not private wallet secrets.

Useful non-private material includes:

- `blk*.dat` files, especially data extending beyond height 175168;
- `blocks/` directories;
- block-index or chainstate archives;
- block height/hash pairs later than 175168;
- transaction IDs and public addresses;
- historical explorer exports;
- old public binaries and source archives;
- archived node information and technical documentation.

## Reachability verification

The endpoint was externally tested from an independent Internet host after deployment of the validated snapshot on 14 September 2026. TCP connections to `81.130.208.151:23247` were accepted successfully.

The permanent node is configured to start automatically and remain available for historical-peer discovery and archival access.

## Recovery policy

If a historical peer supplies later headers or blocks, the project will preserve the received data before analysis and compare it against the recovered genesis, validated height-175168 snapshot, recovered consensus rules and independent historical evidence.

No received continuation will be declared authoritative merely because it is longer or because a peer supplied it. Historical continuity and consensus validity must both be established.

See also:

- [`HISTORICAL_CHAIN_RECOVERY.md`](HISTORICAL_CHAIN_RECOVERY.md)
- [`CHAIN_IDENTITY.md`](CHAIN_IDENTITY.md)
- [`GENESIS_REPRODUCTION.md`](GENESIS_REPRODUCTION.md)
- [`NETWORK_REVIVAL_POLICY.md`](NETWORK_REVIVAL_POLICY.md)
- [`RECONSTRUCTION_POLICY.md`](RECONSTRUCTION_POLICY.md)
- [`EVIDENCE_REGISTER.md`](EVIDENCE_REGISTER.md)

---

**Validated history is being preserved. Later history remains open to evidence.**
