# AML Bitcoin, AMLToken and ABTC — Identity and Historical Context

> This page exists to prevent confusion between the recovered historical AMLToken/ABTC blockchain, the later advertised AML Bitcoin system, later projects using the same ticker, and the legal history surrounding AML Bitcoin.

Repository-wide wording is governed by [`SCOPE_AND_TERMINOLOGY.md`](SCOPE_AND_TERMINOLOGY.md).

## Short version

**AMLToken Revival is an independent technical preservation project for the original native AMLToken/ABTC precursor blockchain.**

It is not affiliated with, endorsed by, or operated by the former AML Bitcoin / AMLToken operators or NAC Foundation.

The project does **not** claim that ABTC currently has a liquid market price, an active exchange market, or present-day commercial value.

What the project has established is technical and historical: the original native AMLToken/ABTC precursor blockchain has been recovered and validated from its original mainnet genesis through at least block **175168**, including fresh full reindexes on three separate project-controlled machines.

That recovered chain is not an ERC-20 or BEP-20 replacement token and is not identified by an Ethereum or BNB Chain contract address.

## The recovered ABTC chain is not the later promised AML Bitcoin system

This distinction is central to the scope of the revival project.

The SEC's 2020 complaint states that purchasers in the offering would first receive **ABTC tokens** that could be traded on various platforms but **would not have the advertised AML Bitcoin features**. According to the complaint, NAC represented that those ABTC tokens could later be exchanged one-for-one for functional AML Bitcoin tokens once a new blockchain and the later tokens were ready.

The SEC separately alleged that NAC and Andrade marketed AML Bitcoin as having anti-money-laundering, anti-terrorism, theft-resistant and biometric-identification capabilities on a "privately regulated public blockchain", while in reality the touted capabilities did not exist and development of AML Bitcoin and its blockchain was still in a very early stage.

Primary SEC sources:

- [SEC complaint — SEC v. NAC Foundation, LLC and Rowland Marcus Andrade](https://www.sec.gov/files/litigation/complaints/2020/comp-pr2020-145-nac-andrade.pdf)
- [SEC press release — SEC Charges Issuer, CEO, and Lobbyist With Defrauding Investors in AML BitCoin](https://www.sec.gov/newsroom/press-releases/2020-145)

The recovered blockchain documented by this repository is therefore framed narrowly as the **historical AMLToken/ABTC precursor chain actually represented by the surviving software and block data**.

AMLToken Revival does **not** claim that the later advertised AML Bitcoin system was completed, does not attribute its promised biometric/AML/KYC or proprietary compliance features to the recovered chain, and does not treat recovery of the ABTC precursor ledger as proof that the later marketed technology existed.

If the historical ABTC chain is eventually modernised and continued, any future engineering work will be documented as a forward revival of this recovered precursor chain. It will not be presented as restoration of proprietary AML Bitcoin capabilities that have not been independently demonstrated from surviving technical evidence.

## The legal history and the blockchain are separate questions

The history of the original AML Bitcoin project includes serious criminal proceedings.

In March 2025, a federal jury convicted Rowland Marcus Andrade of wire fraud and money laundering in connection with the marketing and sale of AML Bitcoin. In July 2025, the U.S. District Court sentenced him to **84 months (seven years) in federal prison**.

The U.S. Department of Justice states that evidence presented at trial showed false representations concerning the development of the technology, its viability, potential business deals and release date.

Primary DOJ sources:

- [DOJ — Founder And CEO Of AML Bitcoin Sentenced To Seven Years In Prison For Multi-Million-Dollar Fraud Scheme](https://www.justice.gov/usao-ndca/pr/founder-and-ceo-aml-bitcoin-sentenced-seven-years-prison-multi-million-dollar-fraud)
- [DOJ — Cryptocurrency Founder And CEO Convicted Of Wire Fraud And Money Laundering In Connection With Marketing And Sale Of AML Bitcoin](https://www.justice.gov/usao-ndca/pr/cryptocurrency-founder-and-ceo-convicted-wire-fraud-and-money-laundering-connection)

AMLToken Revival does not dispute, minimise or attempt to rehabilitate that history.

The technical recovery question is different: **did the original AMLToken/ABTC precursor blockchain exist, and can its historical ledger be preserved and authenticated without rewriting ownership?**

The recovered evidence shows that such a chain did exist. The project has preserved the original genesis, recovered historical blocks and consensus behaviour, and validated the chain through height 175168 on three separate project-controlled machines.

See [`HISTORICAL_CHAIN_RECOVERY.md`](HISTORICAL_CHAIN_RECOVERY.md) for the technical evidence and [`INDEPENDENT_REPRODUCTION.md`](INDEPENDENT_REPRODUCTION.md) for the distinction between project-controlled multi-host reproduction and future independent third-party replication.

## ABTC is an ambiguous ticker

The ticker **ABTC** has been used by unrelated projects. A matching ticker alone does not identify the historical AMLToken blockchain.

For example, the Ethereum contract:

```text
0xe141f43c9022805e10b0a220a8df4936184ea6a4
```

is identified by Etherscan as **American Bitcoin (ABTC)**. It is an ERC-20 token and is **not** the historical AMLToken/ABTC blockchain recovered by this project.

Reference:

- [Etherscan — American Bitcoin (ABTC) contract](https://etherscan.io/address/0xe141f43c9022805e10b0a220a8df4936184ea6a4)

Do not use an unrelated ABTC contract address to determine ownership or balance on the recovered AMLToken chain.

## What identifies the recovered AMLToken chain?

The recovered historical network has its own native blockchain identity.

```text
mainnet genesis:
00000000230d6b389555e80e4523a32343531448ddd15fbc29c0fdc11dbb1538

latest authenticated recovered snapshot height:
175168

snapshot best block hash:
000000008be329b7f5186e61c86367ece62db781374cc7c4fee46ba296b40025

P2P port:
23247
```

The preserved historical raw block file used for validation has SHA256:

```text
77b005775f3d87429571a52b491aeadd0787b3350b3b96249fb1a169964cbf03
```

These chain-level identifiers, together with the preserved original software and repeated project-controlled full-reindex validation, are what identify the historical network.

## What the revival project is — and is not

AMLToken Revival is:

- a preservation and historical-chain recovery effort for the native AMLToken/ABTC precursor chain;
- evidence-led and intended to be independently reproducible;
- committed to keeping the original genesis, historical transactions and ownership unchanged;
- attempting to locate any surviving chain history later than height 175168;
- operating walletless, non-mining archival/discovery nodes to assist that recovery.

AMLToken Revival is **not**:

- the former AML Bitcoin company or its operators;
- an endorsement of the original project's business conduct;
- a claim that the later advertised AML Bitcoin technology was completed;
- an attempt to recreate or claim the promised biometric, AML/KYC, anti-terrorism or theft-resistant proprietary features;
- a replacement token or newly created ledger;
- an ERC-20 or BEP-20 contract;
- a claim that ABTC presently has a market price or liquid exchange market;
- an invitation to trade, invest or deposit funds.

## Market value versus ledger existence

A blockchain balance and a market price are different things.

The project can authenticate historical ledger data without claiming that the asset has a current monetary value or functioning market.

At this stage the project makes **no representation about present-day price, liquidity, exchange support or future value**. Those questions are outside the historical recovery evidence and would depend on any future network revival and market participation.

## Historical holders

If you still possess an old AMLToken wallet, do not use unrelated modern ABTC contract pages to determine what your historical wallet contains.

Start with the holder guide:

**[Old AMLToken / ABTC Wallet — Simple Connection Guide](OLD_WALLET_CONNECTION_GUIDE.md)**

Never publish or send your `wallet.dat`, private keys, seed phrase, wallet passphrase, `dumpwallet` output or `dumpprivkey` output.

## Current recovery boundary

Height **175168** is the latest authenticated historical snapshot currently recovered. It is **not being claimed as the final historical network tip**.

Any later chain data must link correctly to the authenticated snapshot and pass the recovered original consensus rules before it is treated as authentic historical continuation.

For the current public recovery endpoints, see [`PUBLIC_DISCOVERY_NODE.md`](PUBLIC_DISCOVERY_NODE.md).

---

**The legal history is part of the record. The precursor blockchain history is also part of the record. This project preserves the latter without rewriting it, endorsing the former operators, or reviving unverified marketing claims about the later AML Bitcoin system.**