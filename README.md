# AMLToken Revival

> **Public Technical Preview — updated 14 September 2026**

AMLToken Revival is an independent preservation and recovery project for the historical native **AMLToken/ABTC precursor blockchain**.

The project has recovered and validated an authenticated historical AMLToken/ABTC snapshot from the original mainnet genesis through block **175168**, including fresh full reindexes on three separate project-controlled machines.

This repository exists to preserve the technical evidence, document the reconstruction, help locate any later surviving historical chain data, and restore network access without rewriting historical ownership.

## Important status

**This is not a replacement blockchain and it is not a new token launch.**

The recovered snapshot validates the original AMLToken ledger through height **175168**. That height is the latest authenticated snapshot currently recovered; it is **not being claimed as the final historical network tip**.

The preservation rules remain unchanged:

- no replacement production history will be mined from genesis;
- no balances will be recreated by hand;
- no historical ownership will be rewritten;
- later chain data will not be treated as authentic merely because it is longer;
- any continuation beyond height 175168 must independently satisfy chain continuity and consensus validation.

The project rule is simple:

**Same genesis. Same historical ledger. Same ownership.**

## AML Bitcoin, AMLToken and ABTC — important clarification

The ticker **ABTC** is ambiguous and is also used by unrelated modern projects. AMLToken Revival concerns the **original native AMLToken/ABTC precursor blockchain** recovered from preserved historical software and blockchain data. It is not an ERC-20 or BEP-20 replacement token.

The project is independent of the former AML Bitcoin / AMLToken operators and NAC Foundation. It does not dispute or minimise the criminal proceedings connected with the original project's management, and it makes **no claim that ABTC currently has a liquid market price or active exchange market**.

There is also an important historical distinction between the chain recovered here and the later system marketed as **AML Bitcoin**. The SEC's 2020 complaint states that purchasers would first receive tradable ABTC tokens that did not have the advertised AML Bitcoin features and were told those tokens could later be exchanged one-for-one for functional AML Bitcoin tokens once a new blockchain and tokens were ready. The SEC separately alleged that the touted AML Bitcoin capabilities did not exist and that development of AML Bitcoin and its blockchain was still in a very early stage.

Accordingly, recovery of the historical AMLToken/ABTC chain does **not** establish that the later advertised biometric, AML/KYC, anti-terrorism, theft-resistant or other proprietary AML Bitcoin technology was completed. Those claims are outside the recovered technical evidence and are not being revived or adopted by this project.

The legal history, precursor-chain distinction, ticker confusion and technical chain identity are explained separately here:

**[AML Bitcoin, AMLToken and ABTC — Identity and Historical Context](docs/ABTC_IDENTITY_AND_CONTEXT.md)**

Repository-wide wording and terminology are governed by **[Scope and Terminology](docs/SCOPE_AND_TERMINOLOGY.md)**.

## Validated historical snapshot

Current authenticated chain state:

```text
height: 175168
bestblockhash: 000000008be329b7f5186e61c86367ece62db781374cc7c4fee46ba296b40025
genesis: 00000000230d6b389555e80e4523a32343531448ddd15fbc29c0fdc11dbb1538
```

The preserved raw historical block file used for validation has SHA256:

```text
77b005775f3d87429571a52b491aeadd0787b3350b3b96249fb1a169964cbf03
```

Fresh full reindexes on **three separate project-controlled machines** reproduced the same height, tip and genesis without consensus rejection.

See [`docs/HISTORICAL_CHAIN_RECOVERY.md`](docs/HISTORICAL_CHAIN_RECOVERY.md) for the recovery and validation record.

## Independent reproducibility

The project deliberately distinguishes between **multi-host reproduction under project control** and **independent third-party reproduction**.

The three completed full reindexes are strong internal cross-checks, but they are not being presented as third-party replication. A complete outsider replay from GitHub alone is not yet possible because the exact clean reconstruction source tree used for validation and the preserved public historical `blk00000.dat` still need to be published in durable public form.

The target is simple:

**Do not trust our result. Reproduce it.**

The public reproducibility framework, expected hashes and verification standard are documented in [`docs/INDEPENDENT_REPRODUCTION.md`](docs/INDEPENDENT_REPRODUCTION.md). Publication of the remaining artefacts and the first unaffiliated reproduction are tracked in [GitHub Issue #3](https://github.com/Xnuva-Blockchain-Project/AMLToken-Revival/issues/3).

Until an independent reviewer completes that process, this project will not describe the recovery as independently third-party reproduced.

## Public historical-chain archival/discovery nodes

Two public, walletless and non-mining AMLToken recovery nodes are now available on separate networks:

```text
Primary (T620):        81.130.208.151:23247
Secondary (Contabo):  84.247.164.62:23247
```

Both serve the validated historical snapshot through block **175168** and remain available for compatible historical AMLToken nodes that may possess later chain data.

Surviving historical AMLToken nodes may connect to either endpoint using:

```text
addnode=81.130.208.151:23247
addnode=84.247.164.62:23247
```

Both endpoints have been externally verified as reachable from the other network.

The two public nodes are operated independently. Later peer-supplied data is candidate continuation evidence until it has been preserved and independently validated; a longer chain is not accepted as historical truth merely because it was received over P2P.

See [`docs/PUBLIC_DISCOVERY_NODE.md`](docs/PUBLIC_DISCOVERY_NODE.md) for current node status, connection guidance and safety notes.

### I still have an old AMLToken wallet — what should I do?

If you are an old AMLToken/ABTC holder and do not know how to find the wallet data folder or configure a connection, use the simple holder guide:

**[Old AMLToken / ABTC Wallet — Simple Connection Guide](docs/OLD_WALLET_CONNECTION_GUIDE.md)**

It covers Windows, Linux and macOS, explains how to back up the old data before changing anything, and shows how to add both recovery nodes. It also explains what private wallet information must never be uploaded or shared.

## What has been recovered

Evidence-led reconstruction has established:

- preserved original AMLToken-Qt v1.3.0 Windows and Linux artefacts with cryptographic hashes;
- the exact original AMLToken mainnet genesis block;
- the historical network message magic and default P2P port;
- Bitcoin-style SHA256d proof of work and recovered difficulty behaviour;
- compatibility of a preserved historical Berkeley DB wallet with the original client;
- the strongest known Bitcoin Core upstream baseline used by the original software;
- the original AMLToken monetary limits, subsidy behaviour and 20-block coinbase maturity from preserved binary evidence;
- an authenticated raw historical blockchain from genesis through height 175168;
- three fresh full reindexes on separate project-controlled machines reaching the same recovered state;
- two independently reachable public archival/discovery nodes on separate networks;
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

## The remaining historical-chain question

The principal recovery target is now **chain data later than block 175168**.

If you operated AMLToken in 2017–2019, an old computer, disk image, backup, VPS snapshot, exchange node, pool server or archived data directory may contain useful blockchain data such as:

```text
.amltoken/
blocks/
blk*.dat
chainstate/
peers.dat
```

Particularly useful evidence includes:

- `blk*.dat` data extending beyond height 175168;
- block height/hash pairs later than 175168;
- later block-index or chainstate archives;
- historical explorer exports;
- old node backups and VPS snapshots;
- archived node IPs or public technical records.

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

- [`docs/SCOPE_AND_TERMINOLOGY.md`](docs/SCOPE_AND_TERMINOLOGY.md) — canonical project scope and wording rules separating the historical AMLToken/ABTC precursor chain from the later advertised AML Bitcoin system;
- [`docs/ABTC_IDENTITY_AND_CONTEXT.md`](docs/ABTC_IDENTITY_AND_CONTEXT.md) — clarification of the historical AMLToken/ABTC precursor chain, the later advertised AML Bitcoin system, legal context, ticker confusion and unrelated modern ABTC tokens;
- [`docs/OLD_WALLET_CONNECTION_GUIDE.md`](docs/OLD_WALLET_CONNECTION_GUIDE.md) — simple Windows/Linux/macOS instructions for old wallet holders who want to connect safely to the recovery nodes;
- [`docs/INDEPENDENT_REPRODUCTION.md`](docs/INDEPENDENT_REPRODUCTION.md) — public reproducibility standard, expected hashes and the boundary between project-controlled validation and true third-party reproduction;
- [`docs/CHAIN_IDENTITY.md`](docs/CHAIN_IDENTITY.md) — recovered chain identity and mainnet parameters;
- [`docs/GENESIS_REPRODUCTION.md`](docs/GENESIS_REPRODUCTION.md) — deterministic reproduction of the original genesis;
- [`docs/HISTORICAL_CHAIN_RECOVERY.md`](docs/HISTORICAL_CHAIN_RECOVERY.md) — recovered snapshot identity, consensus reconstruction and validation;
- [`docs/EVIDENCE_REGISTER.md`](docs/EVIDENCE_REGISTER.md) — evidence provenance and verification status;
- [`docs/MINING_EVIDENCE.md`](docs/MINING_EVIDENCE.md) — mining and proof-of-work evidence;
- [`docs/RUNTIME_NETWORK_EVIDENCE.md`](docs/RUNTIME_NETWORK_EVIDENCE.md) — original runtime network/consensus fingerprints;
- [`docs/HISTORICAL_NETWORK_CONTROL_EVIDENCE.md`](docs/HISTORICAL_NETWORK_CONTROL_EVIDENCE.md) — recovered authorized-peer mechanism and call-site analysis;
- [`docs/NETWORK_REVIVAL_POLICY.md`](docs/NETWORK_REVIVAL_POLICY.md) — decentralized revival networking policy;
- [`docs/PUBLIC_DISCOVERY_NODE.md`](docs/PUBLIC_DISCOVERY_NODE.md) — public historical-chain endpoints and connection guidance;
- [`docs/UPSTREAM_BASELINE.md`](docs/UPSTREAM_BASELINE.md) — strongest identified upstream Bitcoin Core baseline;
- [`docs/RECONSTRUCTION_POLICY.md`](docs/RECONSTRUCTION_POLICY.md) — holder-protection and continuity rules;
- [`docs/PROJECT_CHECKPOINT_2026-09-14.md`](docs/PROJECT_CHECKPOINT_2026-09-14.md) — earlier project checkpoint preserved as a dated record.

## Current engineering status

The reconstructed node validates the recovered historical ledger from genesis through block 175168.

A clean reconstruction build was used to perform fresh full reindexes on three separate project-controlled machines. All three reached the exact same authenticated tip with no consensus rejection. Independent third-party reproduction remains an explicit open milestone rather than a completed claim.

Two public archival/discovery endpoints are operating:

```text
81.130.208.151:23247
84.247.164.62:23247
```

They are walletless, non-mining and serve working copies of the validated snapshot. Separate canonical snapshots are retained as archival evidence so later P2P activity cannot alter the recovered baseline.

Mainnet discovery seeds are not being invented as a substitute for historical evidence. The public nodes accept compatible inbound connections, while later chain data remains subject to independent preservation and validation.

The current inherited Bitcoin testnet configuration is **not** treated as historical AMLToken testnet identity.

## How to help

The most useful contribution now is evidence that may extend or independently corroborate the recovered chain: later blockchain data, archived public source material, old installation packages, historical node information, block explorers, transaction records or verifiable technical documentation.

Independent reviewers are also invited to follow [`docs/INDEPENDENT_REPRODUCTION.md`](docs/INDEPENDENT_REPRODUCTION.md) and [Issue #3](https://github.com/Xnuva-Blockchain-Project/AMLToken-Revival/issues/3) as the self-contained replay package is completed.

If you still have an old wallet, start with the [simple connection guide](docs/OLD_WALLET_CONNECTION_GUIDE.md). Please use [GitHub Issue #2](https://github.com/Xnuva-Blockchain-Project/AMLToken-Revival/issues/2) for non-private historical-chain evidence or leads. **Do not attach wallet files or private keys.**

## Independence

AMLToken Revival is an independent preservation project. It is **not affiliated with, endorsed by, or operated by** the original AMLToken, AML Bitcoin, NAC Foundation, or their former operators.

For legal-history, precursor-chain and ticker-identity clarification, see [`docs/ABTC_IDENTITY_AND_CONTEXT.md`](docs/ABTC_IDENTITY_AND_CONTEXT.md).

## Release status

This repository remains a **technical/evidence preview**. Recovery of an authenticated snapshot does not make this an invitation to trade, mine replacement history, deposit funds, assume that height 175168 was the final historical network tip, or treat the later advertised AML Bitcoin proprietary features as recovered technology.

See [`RELEASE_NOTES_2026-09-14.md`](RELEASE_NOTES_2026-09-14.md) for the preview release summary and recovery update.

---

**Preserve the evidence. Recover the history. Restore the network without rewriting ownership or reviving unverified marketing claims.**