# AMLToken Revival — Reconstruction Branch

> **Engineering branch — not the authoritative public project-status page.**
>
> Current project status, recovery results and terminology are maintained on the [`main` branch README](https://github.com/Xnuva-Blockchain-Project/AMLToken-Revival/blob/main/README.md).
>
> The project concerns the historical native **AMLToken/ABTC precursor chain** represented by surviving C++ AMLToken software and recovered block data. It does **not** claim to have recovered, completed or authenticated the later advertised AML Bitcoin system with biometric identification, AML/KYC, anti-terrorism, theft-resistant or other proprietary features. See the authoritative [`SCOPE_AND_TERMINOLOGY.md`](https://github.com/Xnuva-Blockchain-Project/AMLToken-Revival/blob/main/docs/SCOPE_AND_TERMINOLOGY.md) and [`ABTC_IDENTITY_AND_CONTEXT.md`](https://github.com/Xnuva-Blockchain-Project/AMLToken-Revival/blob/main/docs/ABTC_IDENTITY_AND_CONTEXT.md).

## Purpose of this branch

This branch preserves reconstruction-era engineering records and source-line work used to recover the historical AMLToken/ABTC precursor chain from evidence.

It must not be read as a current project-status snapshot. Some older commits and documents on this branch predate later breakthroughs, including recovery of authenticated historical block data through height **175168**, deployment of two public archival/discovery nodes, and publication of the independent-reproduction framework.

The authoritative current recovery record is:

- [`main/docs/HISTORICAL_CHAIN_RECOVERY.md`](https://github.com/Xnuva-Blockchain-Project/AMLToken-Revival/blob/main/docs/HISTORICAL_CHAIN_RECOVERY.md)
- [`main/docs/EVIDENCE_REGISTER.md`](https://github.com/Xnuva-Blockchain-Project/AMLToken-Revival/blob/main/docs/EVIDENCE_REGISTER.md)
- [`main/docs/INDEPENDENT_REPRODUCTION.md`](https://github.com/Xnuva-Blockchain-Project/AMLToken-Revival/blob/main/docs/INDEPENDENT_REPRODUCTION.md)

## Preservation rule

**Same genesis. Same historical ledger. Same ownership.**

Reconstruction work must not:

- create a replacement genesis block;
- arbitrarily issue coins or recreate balances by hand;
- rewrite legitimate historical transactions;
- require holders to surrender private keys;
- substitute the later Go/Skycoin-derived AML Bitcoin codebase for the historical C++ AMLToken/ABTC precursor ledger;
- attribute the later advertised AML Bitcoin proprietary features to the recovered precursor chain without independent technical evidence.

Any future modernisation must be forward-only revival-era engineering of the recovered precursor chain and must not retroactively alter historical ownership or be presented as restoration of unverified former marketing claims.

## Current validated historical boundary

The project has authenticated the historical AMLToken/ABTC precursor chain through:

```text
height: 175168
bestblockhash: 000000008be329b7f5186e61c86367ece62db781374cc7c4fee46ba296b40025
genesis: 00000000230d6b389555e80e4523a32343531448ddd15fbc29c0fdc11dbb1538
chainwork: 00000000000000000000000000000000000000000000000000048f2b9dfa1d51
```

Height 175168 is the latest authenticated snapshot currently recovered. It is **not** claimed as the final historical network tip.

The recovered snapshot has been fully reindexed on three separate **project-controlled** machines. Independent third-party reproduction is not yet claimed; see the main-branch reproduction document above.

## Holder safety

Historical holders should **never publish or submit** wallet files, private keys, seed phrases, wallet passphrases, `dumpwallet`, or `dumpprivkey` output.

Public addresses, transaction IDs, block hashes and non-private blockchain data may be used as evidence.

## Independence

AMLToken Revival is an independent preservation project. It is **not affiliated with, endorsed by, or operated by** the former AMLToken / AML Bitcoin operators, NAC Foundation, or their former representatives.

---

**For current status and wording, use `main`. This branch is an engineering record, not a marketing or historical-authority statement.**