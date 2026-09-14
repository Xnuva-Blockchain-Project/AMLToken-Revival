# AMLToken Revival

> **Public Technical Preview — 14 September 2026**

AMLToken Revival is an independent preservation and recovery project for the original **AMLToken (ABTC)** blockchain.

This public preview is being released so historical holders, researchers, developers and anyone who may still possess old AMLToken data can see what has been recovered and help locate the missing historical blockchain.

## Important status

**This is not a live replacement blockchain and it is not a new token launch.**

The project has recovered and independently reproduced important parts of the original AMLToken network identity, but the legitimate post-genesis historical blockchain has **not yet been recovered**. For that reason:

- no replacement production chain will be mined from genesis;
- no balances will be recreated by hand;
- no historical ownership will be rewritten;
- no public release should be represented as an authoritative live AMLToken network yet.

The preservation rule is simple:

**Same genesis. Same historical ledger. Same ownership.**

## Public historical-chain discovery node

A public, walletless and non-mining AMLToken recovery node is now available at:

```text
81.130.208.151:23247
```

Its sole purpose is to help locate surviving historical AMLToken peers and recover the legitimate post-genesis blockchain. The node currently remains deliberately at the recovered original genesis with `blocks: 0` and `headers: 0`; it does not mine or manufacture replacement history.

Surviving historical AMLToken nodes may connect using:

```text
addnode=81.130.208.151:23247
```

Any historical headers or blocks received from a peer must still pass normal consensus and continuity checks before being treated as recovered chain history.

See [`docs/PUBLIC_DISCOVERY_NODE.md`](docs/PUBLIC_DISCOVERY_NODE.md) for status, connection guidance and safety notes.

## What has been recovered

Evidence-led reconstruction has established:

- preserved original AMLToken-Qt v1.3.0 Windows and Linux artefacts with cryptographic hashes;
- the exact original AMLToken mainnet genesis block;
- the historical network message magic and default P2P port;
- Bitcoin-style SHA256d proof of work and recovered difficulty behaviour;
- compatibility of a preserved historical Berkeley DB wallet with the original client;
- the strongest known Bitcoin Core upstream baseline used by the original software;
- an historical operator-defined peer-control mechanism based on `PeerAllowed()` and `pnSeed6_authorized`;
- exactly five direct `PeerAllowed()` call sites affecting outbound connection progression, eviction/retention treatment, address-message processing, block-message processing and compact-block processing;
- a decentralized revival networking path in which ordinary compatible peers can complete a full protocol-70015 handshake without the historical authorization gate.

The recovered mainnet genesis is:

```text
00000000230d6b389555e80e4523a32343531448ddd15fbc29c0fdc11dbb1538
```

## Historical network-control finding

Static analysis of the preserved original AMLToken-Qt v1.3.0 Linux binary established that the historical software contained both a normal fixed-seed table and a separate **authorized-peer table**.

The original client actively consulted that authorized list through `PeerAllowed()` in the normal outbound connection path and in several later peer/message-processing paths.

The revival does **not** recreate that operator-controlled authorization requirement. Seed infrastructure in any future revival will be for discovery only and will not receive consensus, connection, eviction or message-processing privilege.

This finding is documented from preserved binary evidence. The project does not infer developer motive beyond what the software itself proves.

See:

- [`docs/HISTORICAL_NETWORK_CONTROL_EVIDENCE.md`](docs/HISTORICAL_NETWORK_CONTROL_EVIDENCE.md)
- [`docs/NETWORK_REVIVAL_POLICY.md`](docs/NETWORK_REVIVAL_POLICY.md)

## The missing piece: historical chain data

The principal blocker is the legitimate **post-genesis AMLToken/ABTC blockchain**.

If you operated AMLToken in 2017–2019, an old computer, disk image, backup, VPS snapshot or archived data directory may contain useful blockchain data such as:

```text
.amltoken/
blocks/
blk*.dat
chainstate/
peers.dat
```

If you find candidate historical blockchain data, preserve it before modifying or opening it with newer software. Hashing and read-only analysis should come first.

### Do not publish private wallet material

Historical holders should **never** post or send:

- `wallet.dat`;
- private keys;
- seed phrases;
- wallet passphrases;
- `dumpwallet` or `dumpprivkey` output.

Public addresses, transaction IDs, block hashes and non-private blockchain files can be discussed without exposing private-key material.

## Documentation

The public evidence set currently includes:

- [`docs/CHAIN_IDENTITY.md`](docs/CHAIN_IDENTITY.md) — recovered chain identity and mainnet parameters;
- [`docs/GENESIS_REPRODUCTION.md`](docs/GENESIS_REPRODUCTION.md) — deterministic reproduction of the original genesis;
- [`docs/EVIDENCE_REGISTER.md`](docs/EVIDENCE_REGISTER.md) — evidence provenance and verification status;
- [`docs/MINING_EVIDENCE.md`](docs/MINING_EVIDENCE.md) — mining and proof-of-work evidence;
- [`docs/RUNTIME_NETWORK_EVIDENCE.md`](docs/RUNTIME_NETWORK_EVIDENCE.md) — original runtime network/consensus fingerprints;
- [`docs/HISTORICAL_NETWORK_CONTROL_EVIDENCE.md`](docs/HISTORICAL_NETWORK_CONTROL_EVIDENCE.md) — recovered authorized-peer mechanism and call-site analysis;
- [`docs/NETWORK_REVIVAL_POLICY.md`](docs/NETWORK_REVIVAL_POLICY.md) — decentralized revival networking policy;
- [`docs/PUBLIC_DISCOVERY_NODE.md`](docs/PUBLIC_DISCOVERY_NODE.md) — public historical-chain discovery endpoint and connection guidance;
- [`docs/UPSTREAM_BASELINE.md`](docs/UPSTREAM_BASELINE.md) — strongest identified upstream Bitcoin Core baseline;
- [`docs/RECONSTRUCTION_POLICY.md`](docs/RECONSTRUCTION_POLICY.md) — holder-protection and continuity rules;
- [`docs/PROJECT_CHECKPOINT_2026-09-14.md`](docs/PROJECT_CHECKPOINT_2026-09-14.md) — project state at the September 2026 pause.

## Current engineering status

The reconstructed node has reproduced the exact original genesis in an isolated environment. Two reconstructed nodes have also completed a full ordinary-peer handshake while remaining at height 0 and without mining any replacement history.

A public historical-chain discovery endpoint is now operating at `81.130.208.151:23247`. It is walletless and non-mining and exists solely to accept compatible historical peers and recover legitimate chain data if any surviving node reconnects.

Mainnet discovery seeds are deliberately left empty at this stage. We will not invent historical infrastructure or use new seed nodes as a substitute for recovering the legitimate chain.

The current inherited Bitcoin testnet configuration is **not** treated as historical AMLToken testnet identity.

## How to help

The most useful contribution during this stage is evidence: old blockchain data, archived public source material, old installation packages, historical node information, block explorers, transaction records or verifiable technical documentation.

Please open a GitHub issue for non-private evidence or leads. **Do not attach wallet files or private keys.**

## Independence

AMLToken Revival is an independent preservation project. It is **not affiliated with, endorsed by, or operated by** the original AMLToken, AML Bitcoin, NAC Foundation, or their former operators.

## Release status

This repository is a **technical/evidence preview** intended to build community awareness and locate historical data. It is not an invitation to trade, mine a replacement history, deposit funds, or treat reconstructed balances as authoritative.

See [`RELEASE_NOTES_2026-09-14.md`](RELEASE_NOTES_2026-09-14.md) for the preview release summary.

---

**Preserve the evidence. Recover the history. Restore the network without rewriting ownership.**
