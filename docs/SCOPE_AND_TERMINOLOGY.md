# Scope and Terminology

This page defines the terminology used throughout AMLToken Revival so the recovered historical chain is not confused with later AML Bitcoin marketing claims, unrelated assets using the ticker ABTC, or future revival-era engineering.

## Canonical project scope

AMLToken Revival concerns the **historical native AMLToken/ABTC precursor blockchain** represented by the surviving C++ AMLToken software and recovered block data.

It does **not** claim to have recovered, completed or authenticated the later advertised **AML Bitcoin** system with biometric identification, AML/KYC, anti-terrorism, theft-resistant or other proprietary compliance features.

Recovery of the historical AMLToken/ABTC ledger is evidence that the precursor blockchain existed. It is **not evidence that the later advertised AML Bitcoin capabilities were completed or existed as represented**.

For the legal and historical sources behind this distinction, see [`ABTC_IDENTITY_AND_CONTEXT.md`](ABTC_IDENTITY_AND_CONTEXT.md).

## Terms used in this repository

### Historical AMLToken/ABTC precursor chain

This means the native C++ blockchain recovered from preserved AMLToken software and historical block data, beginning with the verified mainnet genesis:

```text
00000000230d6b389555e80e4523a32343531448ddd15fbc29c0fdc11dbb1538
```

Unless a document explicitly says otherwise, **AMLToken**, **ABTC chain**, **historical chain**, **recovered chain** and **revival chain** refer to this precursor blockchain.

### Later advertised AML Bitcoin system

This means the later product marketed as AML Bitcoin with proprietary identity/compliance capabilities and a proposed later blockchain/token system.

This repository does not treat those advertised capabilities as recovered technology and does not use them as part of the historical AMLToken/ABTC chain identity.

### Later Go/Skycoin-derived AML Bitcoin codebase

A separate later Go/Skycoin-derived codebase exists in the historical record. It is not used as the source of truth for the earlier C++ AMLToken/ABTC precursor ledger and must not be substituted for its genesis, balances or transaction history.

### ABTC ticker

`ABTC` is an ambiguous ticker used by unrelated projects. A matching ticker or modern contract address does not identify the historical AMLToken/ABTC precursor chain.

### Revival / modernisation

In this repository, **revival** or **modernisation** means forward engineering of the recovered AMLToken/ABTC precursor chain while preserving historical consensus and ownership.

It does **not** mean reconstructing, adopting or claiming the later advertised AML Bitcoin proprietary features.

Any future functionality added after the authenticated historical boundary must be documented as **revival-era functionality**, not presented as functionality proven to have existed historically.

## Required wording discipline

Preferred wording includes:

- `historical AMLToken/ABTC precursor chain`;
- `recovered AMLToken/ABTC ledger`;
- `later advertised AML Bitcoin system`;
- `future revival-era change`;
- `project-controlled multi-host validation`;
- `independent third-party reproduction` only after an unaffiliated reviewer has actually completed the public replay procedure.

Avoid wording such as:

- `the AML Bitcoin blockchain has been recovered`;
- `we are reviving AML Bitcoin` without immediately qualifying that this means the historical AMLToken/ABTC precursor chain;
- `the recovered chain includes AML/KYC, biometric or theft-resistant technology`;
- `independently reproduced` when referring only to machines operated by this project.

Quotations from SEC, DOJ, historical marketing material or archived sources may of course use the original terminology, but the surrounding text should preserve the distinction.

## Historical versus revival-era rules

Historical blocks and ownership must remain governed by the evidence-backed historical rules.

If the chain is eventually continued after its genuine historical tip is authenticated, any modern networking, wallet, build-system, explorer, protocol or consensus changes must be clearly labelled as forward revival-era engineering.

No forward change may be described as proof that the former AML Bitcoin operators had already implemented that feature.

## Reproducibility wording

The recovered snapshot has been reindexed successfully on three separate **project-controlled** machines. That is multi-host validation, not independent third-party replication.

The project will use the phrase **independent third-party reproduction** only after an unaffiliated reviewer has reproduced the published result using the public source and historical block data.

See [`INDEPENDENT_REPRODUCTION.md`](INDEPENDENT_REPRODUCTION.md).

---

**Project scope: preserve and, if justified by the evidence, continue the real historical AMLToken/ABTC precursor chain. Do not revive or inherit unverified AML Bitcoin marketing claims.**
