# Evidence Register

This register tracks the technical evidence currently supporting recovery of the historical native **AMLToken/ABTC precursor chain**.

It does not treat recovery of that precursor ledger as evidence that the later advertised AML Bitcoin system or its proprietary biometric/AML/KYC features were completed. See [`SCOPE_AND_TERMINOLOGY.md`](SCOPE_AND_TERMINOLOGY.md) and [`ABTC_IDENTITY_AND_CONTEXT.md`](ABTC_IDENTITY_AND_CONTEXT.md).

## E-001 — Original Windows client

- File: `AMLToken-Qt-1.3.0.exe`
- SHA-256: `39cc74896e0fc6ebf313fe8a880be6f74466f8f4314fdff889a73053c23297dd`
- Format: PE32+ x86-64 Windows GUI executable
- Observed version: AMLToken v1.3.0.0-ge278f86c5 (64-bit)
- State: **VERIFIED ORIGINAL ARTEFACT**

## E-002 — Original Windows package

- File: `AMLToken-Qt-1.3.0-Win10x64.zip`
- SHA-256: `476036079d4999124ac1e120ec400589d012a907abfb38c072930e7ef9669abb`
- State: **VERIFIED ORIGINAL ARTEFACT**

## E-003 — Original Linux client

- File: `AMLToken-Qt`
- SHA-256: `61c61988ef5e672ab3aeaa2dba9410f161907433a96c0755cd6484e78d6089d4`
- Format: ELF64 x86-64
- Historical source-path references point to the AMLCore codebase.
- State: **VERIFIED ORIGINAL ARTEFACT**

## E-004 — Mainnet genesis identity

- Height: `0`
- Hash: `00000000230d6b389555e80e4523a32343531448ddd15fbc29c0fdc11dbb1538`
- Source: direct RPC query against the preserved v1.3.0 client in a fresh isolated datadir, subsequently reproduced from recovered block history
- State: **VERIFIED**

## E-005 — Mainnet parameters recovered from binary analysis

Static analysis of the preserved Linux binary yielded and later validation corroborated:

- `nTime`: `0x59bfb540` (`1505736000`)
- `nBits`: `0x1d00ffff`
- `nNonce`: `0x284c21bb` (`676078011`)
- message start: `0d 1c 81 52`
- mainnet P2P port: `23247`

State: **VERIFIED / CORROBORATED**.

See [`CHAIN_IDENTITY.md`](CHAIN_IDENTITY.md) and [`RUNTIME_NETWORK_EVIDENCE.md`](RUNTIME_NETWORK_EVIDENCE.md).

## E-006 — Historical wallet compatibility

A preserved 2018 Berkeley DB wallet was successfully recognized by the preserved v1.3.0 client in an isolated recovery environment. Holder-specific data are intentionally not recorded in this repository.

State: **VERIFIED COMPATIBILITY EVIDENCE**

## E-007 — Separate later AML Bitcoin codebase and marketed system

The historical `amltoken/amltoken` repository is Go/Skycoin-derived and is not treated as the source of truth for the earlier C++ AMLToken/ABTC precursor ledger.

Separately, the later system marketed as AML Bitcoin with biometric, AML/KYC, anti-terrorism, theft-resistant and other proprietary features is not treated as functionality proven by the recovered precursor chain.

State: **REFERENCE / SCOPE SEPARATION ONLY**

See [`ABTC_IDENTITY_AND_CONTEXT.md`](ABTC_IDENTITY_AND_CONTEXT.md).

## E-008 — Historical authorized-peer tables

Static analysis of the preserved original Linux executable identified two separate 260-byte arrays:

- `pnSeed6_authorized`
- `pnSeed6_main`

Debug information identifies both as `SeedSpec6[13]`, with AMLToken's modified layout:

```cpp
struct SeedSpec6 {
    uint8_t  addr[16];
    uint16_t port;
    uint16_t mask;
};
```

The two arrays contain the same 13 IPv4-mapped addresses. The authorized table uses port `23247` for all recovered entries; the main table uses `23237` for its first entry and `23247` for the remaining entries. Every recovered entry has mask `128`.

Evidence reports:

- `amltoken-fixed-seeds-raw.txt` — SHA-256 `b20be2cef4caf69981e05c28f6d7f9aeb61da1a3564fd35c2161d0516b71a065`
- `amltoken-seedspec6-layout.txt` — SHA-256 `a03e08d242d3b2dcb7ad7fbc68fb0b18e0c0bca1acc800bdd7a08d401d04731d`
- `amltoken-seed-mask-semantics.txt` — SHA-256 `a0ecfec5eb65231a7cd3706eb00ab423f83bdc654eb652cfc6decc0830dc03df`

State: **VERIFIED STATIC BINARY EVIDENCE**

See [`HISTORICAL_NETWORK_CONTROL_EVIDENCE.md`](HISTORICAL_NETWORK_CONTROL_EVIDENCE.md).

## E-009 — `PeerAllowed()` active outbound authorization gate

Disassembly of the preserved original Linux executable shows:

- `CMainParams::CMainParams()` copying `pnSeed6_main` into the chain-parameter vector at offset `+0x248`;
- the same constructor copying `pnSeed6_authorized` into the vector at offset `+0x260`;
- `PeerAllowed(CAddress const&, CChainParams const&)` adding `0x260` to the supplied `CChainParams` pointer, converting that vector and performing a membership search;
- `CConnman::OpenNetworkConnection(...)` consulting `PeerAllowed()` before continuing through the normal outbound connection path.

State: **VERIFIED ACCESS-CONTROL MECHANISM**

This evidence establishes a historical outbound peer-authorization gate. It does not, by itself, establish developer motive or prove a direct authorization check at every inbound TCP accept path.

## E-010 — Decentralized peer-connectivity revival test

Two reconstructed AMLToken nodes were run inside an isolated Linux network namespace with no external default route. They used the exact recovered AMLToken genesis and completed a full two-way protocol-70015 handshake as ordinary peers without `PeerAllowed()` or an authorized-peer list. Both remained at height 0 and no blocks were mined.

- Evidence: `amlcore-peer-handshake-20260913_205259.txt`
- SHA-256: `174b2764550ba6b9c9b8d8239aa8b5774b9a42f24cdd295b92ca3486d3ece3ab`
- State: **VERIFIED CLOSED-NETWORK REVIVAL TEST**

See [`NETWORK_REVIVAL_POLICY.md`](NETWORK_REVIVAL_POLICY.md).

## E-011 — Complete direct `PeerAllowed()` call-site classification

A complete static sweep of the preserved original Linux executable identified exactly five direct calls to `PeerAllowed()`.

DWARF information resolves them to:

- `0x1dcb12` — `CConnman::OpenNetworkConnection(...)`, `src/net.cpp:1982` — outbound connection access control;
- `0x1e082a` — `CConnman::AttemptToEvictConnection()`, `src/net.cpp:963` — peer-eviction protection/privilege;
- `0x20d043` — `ProcessMessage(...)`, `src/net_processing.cpp:1461` — address-message handling;
- `0x2113c4` — `ProcessMessage(...)`, `src/net_processing.cpp:2393` — block-message handling;
- `0x212b5e` — `ProcessMessage(...)`, `src/net_processing.cpp:1956` — compact-block handling.

Evidence reports:

- `amltoken-peerallowed-all-call-sites-20260913_210817.txt` — SHA-256 `e09b05f97e6b480cc98de8ad22a74dc62fa8594718beeda9c4ab6356e2f9371a`
- `amltoken-peerallowed-classification-20260914_120152.txt` — SHA-256 `08f0cf425471d118c7440b21f84ccd03e7e3411668e3a217538873ce6149e219`

State: **VERIFIED COMPLETE DIRECT CALL-SITE MAP**

The calls show authorization affecting connection progression, retention/eviction and three network message-processing regions. They do not establish a consensus bypass, and no such bypass is claimed.

See [`HISTORICAL_NETWORK_CONTROL_EVIDENCE.md`](HISTORICAL_NETWORK_CONTROL_EVIDENCE.md).

## E-012 — Decentralized discovery baseline

A read-only audit of the reconstructed AMLToken source confirmed the current mainnet discovery state:

- default P2P port `23247`;
- no `PeerAllowed` symbol in reconstructed source;
- no `pnSeed6_authorized` symbol in reconstructed source;
- mainnet `vSeeds` explicitly cleared;
- mainnet `vFixedSeeds` explicitly cleared;
- ordinary manual peer support remains inherited through the standard peer-to-peer networking path, including `-addnode`/`addnode` support.

Evidence:

- `amlcore-discovery-baseline-20260914_122106.txt` — SHA-256 `b4957187a8132bb0a2d82bc2b5d45df2081ebc877a07a82ef251071a885284e3`

State: **VERIFIED RECONSTRUCTION BASELINE**

The empty mainnet seed lists are intentional during historical recovery. Future seed infrastructure must be documented as revival discovery infrastructure and must not recreate peer authorization or special consensus/network privileges.

See [`NETWORK_REVIVAL_POLICY.md`](NETWORK_REVIVAL_POLICY.md).

## E-013 — Recovered historical raw blockchain through height 175168

A preserved historical AMLToken data source yielded a raw block stream containing 175169 block records, beginning at the authentic AMLToken genesis and extending through height `175168`.

Recovered state:

```text
height: 175168
genesis: 00000000230d6b389555e80e4523a32343531448ddd15fbc29c0fdc11dbb1538
bestblockhash: 000000008be329b7f5186e61c86367ece62db781374cc7c4fee46ba296b40025
chainwork: 00000000000000000000000000000000000000000000000000048f2b9dfa1d51
```

Preserved raw historical block file:

```text
SHA-256: 77b005775f3d87429571a52b491aeadd0787b3350b3b96249fb1a169964cbf03
```

State: **VERIFIED HISTORICAL BLOCK DATA THROUGH HEIGHT 175168**

Important boundary: height 175168 is the latest authenticated snapshot currently recovered. It is not claimed as the final historical network tip.

See [`HISTORICAL_CHAIN_RECOVERY.md`](HISTORICAL_CHAIN_RECOVERY.md).

## E-014 — Historical monetary rules and coinbase maturity recovered from original binary

Validation of the recovered block history exposed inherited Bitcoin rules that did not match AMLToken history. The original AMLToken-Qt v1.3.0 binary was used to recover the historical rules rather than weakening validation.

Recovered rules include:

- `MAX_MONEY = 200,000,000 * COIN`;
- special height-1 subsidy/allocation of `145,000,000 * COIN`;
- non-height-1 subsidy of 100 base units while the subsidy-interval quotient is at most 63, then zero;
- subsidy interval `800000`;
- `COINBASE_MATURITY = 20` blocks.

State: **VERIFIED BINARY-DERIVED CONSENSUS RULES, CORROBORATED BY FULL REINDEX**

## E-015 — Three-machine full-reindex validation

The complete historical snapshot was freshly reindexed on three separate project-controlled machines using the same clean reconstruction codebase:

- reconstruction/development host;
- T620 archival-node host;
- Contabo secondary archival-node host.

Each run reached height `175168`, the same genesis, the same best block hash and the same chainwork without consensus rejection.

Clean reconstruction source commit used for the validated build:

```text
8b821d120b6331cb9ac83c764863e032f567b776
```

Clean build hashes:

```text
bitcoind:    28bf755af53c784b3ab47d7838c65952d6a97031d103006cf58f893edb4f1aae
bitcoin-cli: 5ca9888fbfd9002fe88d0e441a729f1e5c333c573bb7ff8ef47312b42417bfc0
```

State: **VERIFIED PROJECT-CONTROLLED MULTI-HOST REPRODUCTION**

This is deliberately not described as independent third-party replication because all three machines were operated by the project.

## E-016 — Two public archival/discovery nodes

Two walletless, non-mining public AMLToken recovery nodes operate on separate networks:

```text
81.130.208.151:23247
84.247.164.62:23247
```

Both were externally verified as reachable from the other network and serve working copies of the authenticated historical snapshot.

State: **VERIFIED PUBLIC RECOVERY INFRASTRUCTURE**

See [`PUBLIC_DISCOVERY_NODE.md`](PUBLIC_DISCOVERY_NODE.md).

## E-017 — Public independent-reproduction framework

The project has published an explicit standard for third-party reproduction.

Current status:

- project-controlled three-machine reproduction: **COMPLETE**;
- full public outsider replay from GitHub alone: **NOT YET COMPLETE**;
- independent unaffiliated reproduction: **NOT YET CLAIMED**.

Two public artefacts remain required for a self-contained replay:

1. the exact clean reconstruction source tree corresponding to commit `8b821d120b6331cb9ac83c764863e032f567b776`;
2. the preserved public historical `blk00000.dat` with SHA-256 `77b005775f3d87429571a52b491aeadd0787b3350b3b96249fb1a169964cbf03`.

State: **OPEN REPRODUCIBILITY MILESTONE**

See [`INDEPENDENT_REPRODUCTION.md`](INDEPENDENT_REPRODUCTION.md) and [GitHub Issue #3](https://github.com/Xnuva-Blockchain-Project/AMLToken-Revival/issues/3).

## Current evidence gaps

The principal historical-chain gap is surviving genuine AMLToken/ABTC precursor-chain data later than height **175168**. That height is the latest authenticated snapshot currently recovered, not a claimed final network tip.

The principal reproducibility gap is publication of the exact clean reconstruction source tree and preserved public historical raw block file so an unaffiliated reviewer can perform a complete end-to-end replay without trusting project-operated machines.

Until that external replay occurs, the project will distinguish clearly between **project-controlled multi-host validation** and **independent third-party reproduction**.
