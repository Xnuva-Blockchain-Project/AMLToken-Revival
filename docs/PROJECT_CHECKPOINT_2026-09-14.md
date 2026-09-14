# AMLToken Revival Project Checkpoint — 2026-09-14

> **Historical checkpoint — superseded later on 14 September 2026.** This file is retained as a chronological record of the project state before the historical block data was recovered. Statements below saying the post-genesis chain was still missing or unrecovered are no longer current. The project subsequently authenticated the AMLToken/ABTC precursor chain through height **175168**, deployed two public archival/discovery nodes, and published the updated recovery record in [`HISTORICAL_CHAIN_RECOVERY.md`](HISTORICAL_CHAIN_RECOVERY.md). Current project status is in the repository README.
>
> **Scope note:** this project concerns the historical native **AMLToken/ABTC precursor chain**, not the later advertised AML Bitcoin system or its unverified proprietary features. See [`SCOPE_AND_TERMINOLOGY.md`](SCOPE_AND_TERMINOLOGY.md) and [`ABTC_IDENTITY_AND_CONTEXT.md`](ABTC_IDENTITY_AND_CONTEXT.md).

This checkpoint records the project state before a planned pause of approximately six weeks.

The purpose is to make the reconstruction resumable without relying on memory, guesses or undocumented local state.

## Preservation rule

The project remains governed by one non-negotiable rule:

**Same genesis. Same historical ledger. Same ownership.**

The revival must not:

- create a replacement genesis block;
- recreate balances manually;
- migrate holders onto an invented ledger;
- rewrite legitimate historical transactions;
- change ownership merely to make revival easier;
- mine a replacement production history from height 0 while the legitimate historical chain remains unrecovered.

## What is now established

### Original software provenance

Preserved original AMLToken-Qt v1.3.0 Windows and Linux artefacts have been identified and hashed. The Linux binary contains usable symbol and DWARF information and has been analysed statically without relying on a guessed source tree.

### Upstream baseline

The strongest known upstream Bitcoin Core baseline is commit:

```text
e278f86c536921032e8288625dc5f3af610f2ec8
```

The reconstructed AMLCore source is based on that historical code family plus evidence-backed AMLToken parameters and modern build-compatibility fixes.

### Mainnet identity

The original AMLToken mainnet genesis is reproduced exactly:

```text
00000000230d6b389555e80e4523a32343531448ddd15fbc29c0fdc11dbb1538
```

Recovered and validated mainnet identity includes the historical message start, default port, genesis header values and known consensus parameters documented elsewhere in this repository.

### Proof of work

Static analysis established ordinary Bitcoin-style SHA256d proof of work and standard proof-of-work validation behaviour for the recovered code family. No alternative PoW algorithm has been substituted.

### Runtime genesis validation

The reconstructed headless node has been started in a closed network namespace and reproduced the exact AMLToken genesis at runtime. No public chain was created and no historical wallet was involved.

### Historical wallet compatibility

A preserved historical Berkeley DB wallet was recognized by the preserved original client in an isolated recovery environment. Holder-specific data are intentionally excluded from this repository.

This establishes wallet-format continuity, not independent confirmation that every wallet-local historical transaction is currently unspent on the missing historical chain.

### Historical peer-control mechanism

Static analysis of the preserved original Linux binary established an operator-defined authorization mechanism built around:

```text
PeerAllowed(CAddress const&, CChainParams const&)
pnSeed6_authorized
pnSeed6_main
```

Both historical seed arrays contain 13 entries. `PeerAllowed()` actively consults the authorized table.

A complete direct-call sweep identified five `PeerAllowed()` call sites affecting:

- outbound connection progression;
- peer eviction/retention treatment;
- address-message processing;
- block-message processing;
- compact-block processing.

This is documented in [`HISTORICAL_NETWORK_CONTROL_EVIDENCE.md`](HISTORICAL_NETWORK_CONTROL_EVIDENCE.md).

No claim is made that this proves developer motive or a consensus bypass.

### Revival networking decision

The revival deliberately does **not** reproduce the historical authorized-peer gate.

Two reconstructed nodes completed a full protocol-70015 handshake as ordinary peers in a closed network namespace while remaining at height 0.

The current reconstructed mainnet discovery baseline is:

- P2P port `23247`;
- no `PeerAllowed` implementation;
- no `pnSeed6_authorized` implementation;
- mainnet DNS seeds empty;
- mainnet fixed seeds empty;
- ordinary direct peer connection support retained.

The final discovery rules are recorded in [`NETWORK_REVIVAL_POLICY.md`](NETWORK_REVIVAL_POLICY.md).

### Non-mainnet warning

The evidence-backed reconstruction is currently a **mainnet reconstruction**.

The source tree still contains inherited upstream Bitcoin testnet configuration, including upstream Bitcoin testnet seed material. That has not been established as historical AMLToken testnet identity. It must not be treated as AMLToken historical evidence, and `-testnet` should not be used for AMLToken historical validation until AMLToken-specific testnet evidence is recovered.

Regtest remains an engineering environment only and is not historical mainnet evidence.

## Evidence checkpoints

Important local evidence reports and hashes at this checkpoint:

```text
amlcore-genesis-runtime-20260913_203811.txt
SHA-256 e81a92c0e2f53e9e7ade3fc9bd999f43be0b7238cd12c101cef919ead7ff7e5b

amlcore-peer-handshake-20260913_205259.txt
SHA-256 174b2764550ba6b9c9b8d8239aa8b5774b9a42f24cdd295b92ca3486d3ece3ab

amltoken-fixed-seeds-raw.txt
SHA-256 b20be2cef4caf69981e05c28f6d7f9aeb61da1a3564fd35c2161d0516b71a065

amltoken-seedspec6-layout.txt
SHA-256 a03e08d242d3b2dcb7ad7fbc68fb0b18e0c0bca1acc800bdd7a08d401d04731d

amltoken-seed-mask-semantics.txt
SHA-256 a0ecfec5eb65231a7cd3706eb00ab423f83bdc654eb652cfc6decc0830dc03df

amltoken-peerallowed-all-call-sites-20260913_210817.txt
SHA-256 e09b05f97e6b480cc98de8ad22a74dc62fa8594718beeda9c4ab6356e2f9371a

amltoken-peerallowed-classification-20260914_120152.txt
SHA-256 08f0cf425471d118c7440b21f84ccd03e7e3411668e3a217538873ce6149e219

amlcore-discovery-baseline-20260914_122106.txt
SHA-256 b4957187a8132bb0a2d82bc2b5d45df2081ebc877a07a82ef251071a885284e3
```

The original Linux binary itself remains identified by:

```text
SHA-256 61c61988ef5e672ab3aeaa2dba9410f161907433a96c0755cd6484e78d6089d4
```

## Frozen decisions during the pause

Unless contradictory primary evidence is recovered, the following should be treated as frozen:

1. Do not change the recovered mainnet genesis.
2. Do not change the verified SHA256d proof-of-work path or difficulty rules merely for convenience.
3. Do not recreate the historical `PeerAllowed()` gate.
4. Do not grant revival seed nodes privileged connection, eviction or message-processing status.
5. Do not populate mainnet seed lists with guessed historical infrastructure.
6. Do not mine or publish a replacement production chain from genesis.
7. Do not represent wallet-local transaction records as independently chain-confirmed while the historical post-genesis chain remains missing.
8. Do not request or publish holder private keys, seed phrases, passphrases, wallet files or private-key dumps.
9. Do not treat the inherited upstream Bitcoin testnet configuration as historical AMLToken testnet evidence.

## Principal unresolved blocker

The decisive remaining blocker is the **legitimate historical post-genesis AMLToken/ABTC chain**.

The reconstructed software can reproduce the original genesis and communicate as ordinary peers, but production revival cannot honestly proceed until surviving historical block data, a legitimate historical tip, or other independently verifiable chain evidence is recovered.

The absence of the historical chain must not be solved by inventing one.

## Resume sequence after the pause

When work resumes, use this order:

1. Search surviving disks, backups, archived machines and other lawful sources for historical AMLToken blockchain data such as the original data directory or `blk*.dat` files.
2. Preserve any candidate data read-only and hash it before attempting conversion or loading.
3. Verify candidate blocks against the already recovered genesis, PoW, difficulty and network identity.
4. Determine the legitimate historical tip and whether the known wallet-era transaction history can be independently confirmed against the recovered chain.
5. Only after historical continuity is established, design and deploy multiple revival discovery endpoints as discovery infrastructure rather than authorization authorities.
6. Then perform controlled multi-node synchronization tests against the recovered historical chain before considering any public release.
7. Later work may address GUI branding, historical wallet database compatibility and user-facing installers, but none of those tasks outranks historical chain recovery.

## Current production status

**NOT READY FOR PUBLIC PRODUCTION CHAIN OPERATION.**

The reconstruction is suitable for isolated validation and forensic work. It is not yet an authoritative live replacement network because the legitimate post-genesis history has not been recovered.

---

**Checkpoint principle: preserve evidence first; restore connectivity second; extend the chain only after legitimate history is recovered.**
