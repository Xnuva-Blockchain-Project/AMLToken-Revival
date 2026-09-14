# Public Evidential Findings

> **Transparency principle:** publish the evidence, including findings that are inconvenient, ambiguous, or adverse to assumptions about the historical project. Separate what is proven from what is inferred, and keep private holder material out of the public record.

This document is a consolidated public summary of the principal non-private findings produced by the AMLToken Revival investigation. It does not replace the detailed evidence documents; it provides a single place where researchers can see what has been established, what remains uncertain, and which questions could change the project's conclusions.

Repository-wide terminology is governed by [`SCOPE_AND_TERMINOLOGY.md`](SCOPE_AND_TERMINOLOGY.md).

## Evidence-status vocabulary

The project uses the following evidence states:

- **VERIFIED** — observed directly from preserved original software or historical chain data, or reproduced deterministically from such evidence.
- **EXTRACTED** — recovered by static analysis, disassembly, symbols, DWARF or another direct examination of a preserved original artefact.
- **DERIVED** — calculated deterministically from verified or extracted evidence.
- **CORROBORATED** — supported by more than one independent evidential route.
- **INFERENCE** — a plausible interpretation that remains open to contrary evidence.
- **UNKNOWN / OPEN** — not established and must not be filled in by convenience.

## 1. Historical chain identity — VERIFIED

The recovered chain is the historical native **AMLToken/ABTC precursor blockchain** represented by surviving C++ AMLToken software and historical block data.

Verified mainnet genesis:

```text
00000000230d6b389555e80e4523a32343531448ddd15fbc29c0fdc11dbb1538
```

The genesis block has been reproduced byte-for-byte from preserved original-client data and later recovered again as the first block in the historical raw block stream.

Verified network identity includes:

```text
message start: 0d 1c 81 52
P2P port:     23247
PUBKEY:       0x41
SCRIPT:       0x05
SECRET:       0xc1
```

See [`CHAIN_IDENTITY.md`](CHAIN_IDENTITY.md) and [`GENESIS_REPRODUCTION.md`](GENESIS_REPRODUCTION.md).

## 2. Preserved original software provenance — VERIFIED

Preserved original AMLToken software includes Windows and Linux AMLToken-Qt v1.3.0 artefacts whose cryptographic hashes are recorded in [`EVIDENCE_REGISTER.md`](EVIDENCE_REGISTER.md).

The original runtime reports:

```text
AMLToken v1.3.0.0-ge278f86c5 (64-bit)
```

The build suffix resolves exactly to Bitcoin Core commit:

```text
e278f86c536921032e8288625dc5f3af610f2ec8
```

This is the strongest identified upstream source baseline. It is not assumed that every AMLToken source file was otherwise identical to Bitcoin Core.

See [`UPSTREAM_BASELINE.md`](UPSTREAM_BASELINE.md).

## 3. Historical proof of work and difficulty — VERIFIED / CORROBORATED

The preserved original binary exposes the Bitcoin-Core-style proof-of-work functions `GetNextWorkRequired`, `CalculateNextWorkRequired` and `CheckProofOfWork`.

The genesis header reproduces exactly under Bitcoin SHA-256d, and no separate scrypt, X11 or alternative `GetPoWHash` path was found in the focused original-binary audit.

Recovered mainnet difficulty behaviour uses:

```text
target spacing:  60 seconds
target timespan: 600 seconds
interval:        10 blocks
```

The recovered historical block stream subsequently passed full reindex validation under the reconstructed SHA-256d/difficulty rules.

See [`MINING_EVIDENCE.md`](MINING_EVIDENCE.md).

## 4. Historical monetary rules — VERIFIED / CORROBORATED

Validation of the recovered chain exposed monetary rules that differed from inherited Bitcoin defaults. The preserved original AMLToken binary was used to recover them rather than weakening validation.

Recovered rules include:

```text
COIN = 100000000
MAX_MONEY = 200,000,000 * COIN
subsidy interval = 800000
COINBASE_MATURITY = 20
```

The historical rules also include a special height-1 allocation of `145,000,000 * COIN` and the recovered later subsidy behaviour documented in [`HISTORICAL_CHAIN_RECOVERY.md`](HISTORICAL_CHAIN_RECOVERY.md) and [`EVIDENCE_REGISTER.md`](EVIDENCE_REGISTER.md).

The presence of a 200 million maximum-money rule is technically established from the original binary. Its relationship to statements in historical offering material and regulatory filings about ABTC supply is a separate provenance question and should be compared carefully rather than assumed.

## 5. Historical blockchain recovered through height 175168 — VERIFIED

A preserved historical AMLToken data source yielded a raw block stream containing 175169 records from genesis through height **175168**.

Authenticated recovered state:

```text
height:        175168
bestblockhash: 000000008be329b7f5186e61c86367ece62db781374cc7c4fee46ba296b40025
genesis:       00000000230d6b389555e80e4523a32343531448ddd15fbc29c0fdc11dbb1538
chainwork:     00000000000000000000000000000000000000000000000000048f2b9dfa1d51
```

Preserved raw historical block file SHA-256:

```text
77b005775f3d87429571a52b491aeadd0787b3350b3b96249fb1a169964cbf03
```

Height 175168 is the **latest authenticated snapshot currently recovered**. It is not being claimed as the final historical network tip.

See [`HISTORICAL_CHAIN_RECOVERY.md`](HISTORICAL_CHAIN_RECOVERY.md).

## 6. Full-reindex validation on three project-controlled machines — VERIFIED

The recovered raw history was freshly reindexed on three separate project-controlled systems:

- the reconstruction/development host;
- the T620 archival-node host;
- the Contabo archival-node host.

All three reproduced the same height, genesis, best block hash and chainwork without consensus rejection.

This is **project-controlled multi-host validation**, not independent third-party reproduction.

The project will not use the phrase **independent third-party reproduction** until an unaffiliated reviewer has reproduced the result from the public source and public historical block data.

See [`INDEPENDENT_REPRODUCTION.md`](INDEPENDENT_REPRODUCTION.md) and GitHub Issue #3.

## 7. Historical wallet-format compatibility — VERIFIED, HOLDER-SPECIFIC DETAILS WITHHELD

A preserved historical Berkeley DB wallet was recognized by the preserved original AMLToken-Qt client in an isolated environment.

This establishes historical wallet-format continuity. Holder-specific addresses, balances, private wallet files and other identifying wallet evidence are intentionally not published as part of the public evidential record.

The project never needs private keys, seed phrases, wallet passphrases, `dumpwallet`, `dumpprivkey` or a holder's `wallet.dat` to establish the public chain history.

See [`OLD_WALLET_CONNECTION_GUIDE.md`](OLD_WALLET_CONNECTION_GUIDE.md).

## 8. Historical authorized-peer mechanism — VERIFIED / ADVERSE EVIDENCE INCLUDED

The preserved original Linux binary contains:

```text
pnSeed6_authorized
pnSeed6_main
PeerAllowed(CAddress const&, CChainParams const&)
```

Static analysis recovered two 13-entry historical seed tables and established that `PeerAllowed()` consulted the authorized table.

A complete direct-call sweep found five direct `PeerAllowed()` uses affecting:

- outbound connection progression;
- peer eviction/retention treatment;
- address-message handling;
- block-message handling;
- compact-block handling.

This is evidence that the historical network had an operator-defined peer-control layer that was more centralized than ordinary open Bitcoin-style peer discovery.

It does **not** establish that authorized peers could bypass proof-of-work or consensus validation, and it does not by itself prove how many independent miners or independently operated nodes existed historically.

See [`HISTORICAL_NETWORK_CONTROL_EVIDENCE.md`](HISTORICAL_NETWORK_CONTROL_EVIDENCE.md).

## 9. Historical decentralization — OPEN QUESTION

The existence of a valid blockchain and proof-of-work history does **not** by itself establish that the historical AMLToken/ABTC network was broadly decentralized in operation.

The authorized-peer mechanism gives a concrete reason to investigate this separately.

Questions still open include:

- how many independent entities mined historical blocks;
- whether mining was open to unrelated participants in practice;
- how concentrated historical hash power was;
- whether coinbase outputs or extra-nonce patterns indicate one operator, a small group, pools, or broader miner diversity;
- how many independently operated full nodes existed;
- whether ordinary users could join the network without dependence on operator-controlled infrastructure.

Future analysis of block timing, difficulty changes, coinbase destinations, coinbase scripts, extra-nonce patterns and other public block fingerprints should be published regardless of whether the result supports or weakens a decentralization narrative.

Until that work is complete, the project should say: **historical blockchain existence and PoW validation are established; historical operational decentralization is not yet established.**

## 10. Later advertised AML Bitcoin system — NOT ESTABLISHED BY THE RECOVERED CHAIN

The recovered AMLToken/ABTC precursor chain must not be conflated with the later system marketed as AML Bitcoin with biometric identification, AML/KYC, anti-terrorism, theft-resistant or other proprietary compliance features.

Primary SEC material states that purchasers would initially receive ABTC tokens without the advertised AML Bitcoin features and that a later one-for-one exchange into functional AML Bitcoin tokens was represented for a future stage.

Recovery of the precursor ledger therefore does not prove that the later advertised AML Bitcoin system was completed or possessed those claimed capabilities.

The revival project will not reproduce those advertised features. Any future continuation is intended to be a conventional open peer-to-peer cryptocurrency network, with any new functionality labelled explicitly as revival-era engineering.

See [`ABTC_IDENTITY_AND_CONTEXT.md`](ABTC_IDENTITY_AND_CONTEXT.md) and [`SCOPE_AND_TERMINOLOGY.md`](SCOPE_AND_TERMINOLOGY.md).

## 11. Later Go/Skycoin-derived AML Bitcoin codebase — SEPARATE HISTORICAL ARTEFACT

A later Go/Skycoin-derived AML Bitcoin codebase exists in the historical record.

It is not used as the source of truth for the earlier C++ AMLToken/ABTC precursor chain and must not be substituted for the recovered chain's genesis, balances or transaction history.

The precise historical and operational relationship between the precursor ABTC chain, any proposed conversion process and the later codebase remains a subject for documentary research.

## 12. Regulatory and criminal-case context — PRIMARY SOURCES ACKNOWLEDGED

The project does not dispute or minimise the legal record surrounding the former AML Bitcoin operation.

The repository cites the SEC complaint and SEC press release, together with DOJ conviction and sentencing material. Those sources are used to define the boundary between the precursor ABTC asset/ledger and the later advertised AML Bitcoin system.

Legal allegations and adjudicated conduct are not used as substitutes for technical evidence about individual blocks, consensus rules or peer topology. Conversely, technical recovery of a real blockchain does not negate the legal findings concerning the former operation's marketing and conduct.

See [`ABTC_IDENTITY_AND_CONTEXT.md`](ABTC_IDENTITY_AND_CONTEXT.md).

## 13. Supply and chronology correlations — OPEN FOR PRIMARY-SOURCE CROSS-CHECK

Two historical correlations deserve explicit investigation rather than assumption:

1. The original binary independently establishes a `MAX_MONEY` rule of **200,000,000** coins, while historical offering/regulatory material describes a 200 million ABTC quantity. The numerical correspondence is potentially corroborative but the exact issuance/distribution relationship must be established from primary documents and chain analysis.
2. The recovered native chain begins in September 2017 and the authenticated snapshot reaches March 2018, while regulatory descriptions of token issuance and later exchange trading use their own dates and terminology. Those narratives must be reconciled carefully so that "chain creation", "token issuance to purchasers", "ICO distribution" and "exchange trading" are not incorrectly treated as the same event.

These are provenance questions, not reasons to alter the recovered blockchain.

## 14. Public recovery infrastructure — VERIFIED CURRENT PROJECT INFRASTRUCTURE

Two walletless, non-mining archival/discovery nodes are operated on separate networks:

```text
81.130.208.151:23247
84.247.164.62:23247
```

These are **revival-era recovery endpoints**, not historical proof that the former network used these hosts.

They serve working copies of the authenticated snapshot and remain available to compatible historical peers that may possess later data. Candidate later history is not accepted merely because it is longer; it must link to the authenticated snapshot and pass recovered historical consensus validation.

See [`PUBLIC_DISCOVERY_NODE.md`](PUBLIC_DISCOVERY_NODE.md).

## 15. Historical source reconstruction — EVIDENCE-LED, NOT COMPLETE ORIGINAL SOURCE RECOVERY

The reconstruction starts from the exact identified Bitcoin Core upstream baseline and applies AMLToken-specific differences only where supported by preserved original software, runtime output or recovered historical block data.

The resulting code has validated the recovered historical snapshot, but it is a reconstruction. It must not be represented as a byte-for-byte recovery of the former developers' complete original AMLCore source tree unless that source is actually recovered.

## 16. Current reproducibility gap — OPEN

The project-controlled three-host reindex result is complete, but a stranger cannot yet perform the entire replay from GitHub alone.

The remaining public-package requirements include:

- publication of the exact clean reconstruction source tree corresponding to the validated build;
- publication of the preserved public historical raw block file in durable form;
- exact build/dependency instructions;
- a simple fresh-datadir reproduction procedure;
- at least one unaffiliated third-party reproduction report.

See [`INDEPENDENT_REPRODUCTION.md`](INDEPENDENT_REPRODUCTION.md).

## 17. Principal unresolved historical-chain gap — OPEN

No claim is made that block 175168 is the final historical AMLToken/ABTC precursor-chain tip.

The project continues to seek genuine historical data later than height 175168, including `blk*.dat`, historical node snapshots, explorer records, height/hash pairs and other non-private evidence.

See GitHub Issue #2.

## Publication principle

The project should publish all material findings that can lawfully and safely be made public, including evidence that complicates the revival narrative.

What should be public where possible:

- hashes and provenance of original software artefacts;
- recovered consensus and network parameters;
- deterministic reproduction procedures;
- public historical block data and its hashes;
- static-analysis findings;
- validation failures that led to recovered rules;
- network-centralization evidence;
- contradictory or ambiguous documentary evidence;
- negative findings and unresolved questions;
- methodology and limitations;
- third-party reproduction reports, including failed reproductions when technically informative.

What should **not** be made public merely for transparency:

- private keys, seeds, wallet passphrases or private-key dumps;
- private `wallet.dat` files;
- unnecessary holder-identifying information;
- credentials, RPC secrets, SSH material or infrastructure secrets;
- copyrighted third-party binaries or documents where redistribution is not lawful; hashes, provenance and analysis can still be published.

Transparency does not mean pretending every question is answered. It means making it possible for another researcher to distinguish evidence, interpretation, contradiction and uncertainty.

---

**Project evidential standard: publish what the evidence shows, publish what it does not show, and preserve the distinction between the two.**