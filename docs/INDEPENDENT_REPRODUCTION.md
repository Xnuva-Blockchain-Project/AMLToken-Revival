# Independent Reproduction

> Status: reproduction framework published 14 September 2026. Full third-party end-to-end replay is **not yet complete** because two required public artefacts still have to be published.

## Do not trust our result. Reproduce it.

The strongest test of the AMLToken recovery is whether an independent person can start from the published source and public historical block data, build the node themselves, reindex from an empty data directory, and obtain the same chain state without trusting project-operated binaries or machines.

That is the standard this project intends to meet.

## What has already been reproduced

The authenticated historical snapshot has been freshly reindexed on **three separate machines**:

- the reconstruction/development host;
- the T620 archival-node host;
- the Contabo secondary archival-node host.

All three runs used the same clean reconstruction codebase and the same preserved historical raw block file. Each independently reached the same mainnet state without consensus rejection.

These are valuable independent executions, but all three machines were operated by the project. They therefore **do not count as independent third-party replication**.

## Expected result

A successful independent replay should reproduce:

```text
height: 175168

genesis:
00000000230d6b389555e80e4523a32343531448ddd15fbc29c0fdc11dbb1538

bestblockhash:
000000008be329b7f5186e61c86367ece62db781374cc7c4fee46ba296b40025

chainwork:
00000000000000000000000000000000000000000000000000048f2b9dfa1d51
```

The preserved historical raw block file used by the project has SHA-256:

```text
77b005775f3d87429571a52b491aeadd0787b3350b3b96249fb1a169964cbf03
```

The clean reconstruction source commit used for the validated build is:

```text
8b821d120b6331cb9ac83c764863e032f567b776
```

The clean project binaries produced from that source had the following SHA-256 values:

```text
bitcoind:
28bf755af53c784b3ab47d7838c65952d6a97031d103006cf58f893edb4f1aae

bitcoin-cli:
5ca9888fbfd9002fe88d0e441a729f1e5c333c573bb7ff8ef47312b42417bfc0
```

The Bitcoin-style names above are engineering build names from the reconstruction tree. They are not being presented as the final historical AMLToken executable names.

## Current public reproducibility boundary

A complete outsider replay from GitHub alone is **not yet possible**.

Two artefacts still need to be published in a durable public form:

1. the exact clean reconstruction source tree corresponding to commit `8b821d120b6331cb9ac83c764863e032f567b776`;
2. the preserved public historical `blk00000.dat` whose SHA-256 is `77b005775f3d87429571a52b491aeadd0787b3350b3b96249fb1a169964cbf03`.

The repository already documents the recovered parameters, evidence and validation results, but documentation alone is not a substitute for making those two artefacts independently replayable.

The publication and third-party verification work is tracked in **[GitHub Issue #3](https://github.com/Xnuva-Blockchain-Project/AMLToken-Revival/issues/3)**.

## Required reproduction package

The complete public package should contain:

- the exact reconstruction source tree used for validation;
- exact build/dependency instructions;
- the preserved public historical raw block file or an immutable release download for it;
- the raw block file SHA-256 shown above;
- a small validation script or exact command sequence;
- expected genesis, height, best-block hash and chainwork;
- a statement that the procedure starts from a fresh data directory;
- instructions to perform the replay with networking disabled where practical;
- no holder wallet files or other private material.

## Independent verification procedure

Once the complete package is public, an independent reviewer should:

1. obtain the source from the published immutable revision;
2. compile it themselves rather than trusting a project-supplied executable;
3. verify the SHA-256 of the historical block file;
4. create a brand-new empty AMLToken data directory;
5. place only the public historical block data required for the replay into that clean environment;
6. run a full reindex with networking disabled where practical;
7. allow validation to complete without bypassing consensus checks;
8. record the resulting height, genesis hash, best block hash and chainwork;
9. compare those results with the expected values above;
10. publish enough environment information for somebody else to repeat the test.

A useful independent report should include:

```text
Operating system:
Compiler/toolchain:
Source revision:
Historical block-file SHA-256:
Final height:
Genesis hash:
Best block hash:
Chainwork:
Consensus rejection observed: yes/no
Notes:
```

## What would count as a successful third-party reproduction?

A strong result would be an unaffiliated reviewer, using their own machine and a self-compiled build, reproducing the same chain state from the published historical block file without using project-generated chainstate or block-index databases.

Even stronger would be several reviewers using different distributions or toolchains and reaching the same consensus result.

The purpose is not to obtain agreement by assertion. It is to make disagreement technically testable.

## What this test does and does not prove

A successful replay would strongly corroborate that:

- the published reconstruction accepts the recovered block history under the recovered consensus rules;
- the raw historical block file deterministically leads to the published height, genesis, best-block hash and chainwork;
- the result does not depend on hidden project chainstate or database files.

It would **not**, by itself, prove that height 175168 was the final historical AMLToken network tip. Later genuine historical chain data may still exist and remains a separate recovery question.

It also does not require anybody to expose private wallet material.

## Holder safety

Independent reproduction concerns **public source code and public blockchain data only**.

Never publish or request:

- `wallet.dat`;
- private keys;
- seed phrases;
- wallet passwords or passphrases;
- `dumpwallet` output;
- `dumpprivkey` output.

## Project standard

The project will distinguish clearly between:

- **project-controlled multi-host reproduction** — already achieved on three separate machines; and
- **independent third-party reproduction** — not yet claimed until an unaffiliated reviewer completes the public procedure.

That distinction is deliberate.

---

**Do not trust the recovery because we say it works. Reproduce the evidence and make the result stand on its own.**
