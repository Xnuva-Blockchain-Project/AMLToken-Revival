# Reconstruction and Holder-Protection Policy

AMLToken Revival exists to preserve evidence and, if technically possible, restore the original AMLToken (ABTC) network without rewriting historical ownership.

## Core rule

**Same genesis. Same historical ledger. Same ownership.**

The purpose of reconstruction is continuity, not replacement.

## What this project may do

The project may:

- recover chain parameters from original binaries, source fragments, wallets, blocks and other surviving artefacts;
- reproduce the original node software sufficiently to validate the historical chain;
- modernise build systems, dependencies and user interfaces where that does not alter historical consensus;
- add forward-only safety or maintenance changes after a clearly documented activation point, if required;
- build tools that allow historical holders to prove control of addresses without disclosing private keys;
- document chain evidence so independent researchers can reproduce the findings.

## What this project will not do

The project will not:

- create a new genesis block and call it the original AMLToken chain;
- manually credit claimed balances to a replacement ledger;
- invent transactions to compensate holders;
- alter historical blocks or legitimate historical ownership;
- request or collect private keys, seed phrases, wallet passphrases or private-key dumps;
- publish private wallet files as recovery evidence;
- silently substitute the later AML Bitcoin / Skycoin-derived chain for the original C++ ABTC chain;
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
- clearly distinguished from original historical consensus.

## Evidence discipline

Every reconstructed parameter should be tagged according to its evidence state:

- **VERIFIED** — observed directly from original software or original chain data;
- **EXTRACTED** — recovered by static analysis from an original binary or artefact;
- **DERIVED** — calculated deterministically from verified or extracted data;
- **INFERENCE** — plausible interpretation that still requires corroboration;
- **UNKNOWN** — not yet established.

Unknown values are not to be filled in by convenience.

## Publication gate

The repository should remain private during early reconstruction. Public release should occur only when the project can clearly state which parts of the chain have been independently reproduced, which historical data remain missing, and which behaviours are original versus forward-only revival changes.