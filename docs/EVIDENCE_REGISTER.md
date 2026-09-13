# Evidence Register

This register tracks the technical evidence currently supporting AMLToken reconstruction.

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
- Source: direct RPC query against the preserved v1.3.0 client in a fresh isolated datadir
- State: **VERIFIED**

## E-005 — Mainnet parameters recovered from binary analysis

Static analysis of the preserved Linux binary yielded:

- `nTime`: `0x59bfb540` (`1505736000`)
- `nBits`: `0x1d00ffff`
- `nNonce`: `0x284c21bb` (`676078011`)
- message start: `0d 1c 81 52`
- candidate mainnet port: `0x5acf` (`23247`)

State: **EXTRACTED**. Runtime or historical block-data confirmation is still required where noted in `CHAIN_IDENTITY.md`.

## E-006 — Historical wallet compatibility

A preserved 2018 Berkeley DB wallet was successfully recognized by the preserved v1.3.0 client in an isolated recovery environment. Holder-specific data are intentionally not recorded in this repository.

State: **VERIFIED COMPATIBILITY EVIDENCE**

## E-007 — Separate later AML Bitcoin codebase

The historical `amltoken/amltoken` repository is Go/Skycoin-derived and is not treated as the source of truth for the earlier C++ AMLToken/ABTC ledger.

State: **REFERENCE ONLY**

## Current evidence gap

The principal unresolved item is surviving post-genesis ABTC blockchain data. A complete historical block sequence has not yet been recovered. Until it is, wallet-local transaction records must not be represented as independently chain-confirmed balances.