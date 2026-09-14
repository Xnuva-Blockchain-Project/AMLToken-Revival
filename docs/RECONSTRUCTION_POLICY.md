# Reconstruction and Holder-Protection Policy

AMLToken Revival exists to preserve evidence and, if technically possible, restore and continue the historical native **AMLToken/ABTC precursor chain** without rewriting historical ownership.

This project does **not** treat the recovered precursor chain as proof that the later advertised AML Bitcoin system or its biometric, AML/KYC, anti-terrorism, theft-resistant or other proprietary features were completed. Repository-wide wording follows [`SCOPE_AND_TERMINOLOGY.md`](SCOPE_AND_TERMINOLOGY.md).

## Core rule

**Same genesis. Same historical ledger. Same ownership.**

The purpose of reconstruction is continuity, not replacement.

## What this project may do

The project may:

- recover chain parameters from original binaries, source fragments, wallets, blocks and other surviving artefacts;
- reproduce the original node software sufficiently to validate the historical AMLToken/ABTC precursor chain;
- modernise build systems, dependencies and user interfaces where that does not alter historical consensus;
- add forward-only safety or maintenance changes after a clearly documented activation point, if required;
- build tools that allow historical holders to prove control of addresses without disclosing private keys;
- document chain evidence so independent researchers can reproduce the findings.

Any future modernisation is revival-era engineering of the recovered precursor chain. It must not be presented as restoration of unverified proprietary AML Bitcoin capabilities.

## What this project will not do

The project will not:

- create a new genesis block and call it the original AMLToken chain;
- manually credit claimed balances to a replacement ledger;
- invent transactions to compensate holders;
- alter historical blocks or legitimate historical ownership;
- request or collect private keys, seed phrases, wallet passphrases or private-key dumps;
- publish private wallet files as recovery evidence;
- silently substitute the later AML Bitcoin / Skycoin-derived codebase for the original C++ AMLToken/ABTC precursor chain;
- represent recovery of the precursor ledger as proof that the later advertised AML Bitcoin system was completed;
- attribute biometric, AML/KYC, anti-terrorism, theft-resistant or other proprietary AML Bitcoin claims to the recovered chain without independent technical evidence;
- market the reconstruction as a new investment product or token sale.

## Historical-holder protection

A central reason for this project is that historical purchasers were left with wallets and/or token records that became difficult or impossible to verify through the original infrastructure. Recovery work should therefore maximise evidence preservation and minimise the risk of a second loss.

Holder claims must not be accepted merely from screenshots, account statements or recollection where cryptographic evidence is available. The preferred evidence hierarchy is:

1. original chain data and confirmed historical transactions;
2. control of the original address demonstrated by a signed message or equivalent non-custodial proof;
3. original wallet metadata and raw transactions, handled locally by the holder;
4. documentary evidence only as supporting context.

Private-key material must remain with the holder.

## Consensus-change rule

No consensus change may alter the validity or ownership consequences of legitimate historical blocks before the revival activation point.

If a forward-only change eventually becomes necessary, it must be:

- separately documented;
- activated only after the historical chain has been reconstructed and validated as far as surviving evidence permits;
- deterministic and reviewable;
- incapable of reallocating old balances by administrator decision;
- clearly distinguished from original historical consensus;
- labelled as revival-era functionality rather than attributed retrospectively to the former AML Bitcoin project.

## Evidence discipline

Every reconstructed parameter should be tagged according to its evidence state:

- **VERIFIED** — observed directly from original software or original chain data;
- **EXTRACTED** — recovered by static analysis from an original binary or artefact;
- **DERIVED** — calculated deterministically from verified or extracted data;
- **INFERENCE** — plausible interpretation that still requires corroboration;
- **UNKNOWN** — not yet established.

Unknown values are not to be filled in by convenience.

## Publication and reproducibility standard

The repository is now public as a technical/evidence preview. Public wording must clearly distinguish:

- the historical AMLToken/ABTC precursor chain from the later advertised AML Bitcoin system;
- historical behaviour from forward-only revival changes;
- project-controlled multi-host validation from genuine independent third-party reproduction;
- authenticated history through height 175168 from any later candidate continuation that remains unverified.

Independent third-party reproduction is not claimed until an unaffiliated reviewer completes the public replay procedure described in [`INDEPENDENT_REPRODUCTION.md`](INDEPENDENT_REPRODUCTION.md).