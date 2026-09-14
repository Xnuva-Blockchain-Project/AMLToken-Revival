# AMLToken Network Revival Policy

## Purpose

This document records the networking policy used by the AMLToken revival.

The objective is to restore peer-to-peer availability while preserving the historical AMLToken blockchain, consensus rules, transaction history, balances and private-key ownership.

No new genesis block, balance migration, historical rewrite or replacement ledger is permitted.

## Historical authorized-peer mechanism

Forensic analysis of the preserved original AMLToken-Qt v1.3.0 Linux binary identified:

- `PeerAllowed(CAddress const&, CChainParams const&)`
- `pnSeed6_authorized`
- `pnSeed6_main`

The recovered `SeedSpec6` layout is:

```cpp
struct SeedSpec6 {
    uint8_t  addr[16];
    uint16_t port;
    uint16_t mask;
};
```

Both historical arrays contain 13 entries. The main-network constructor copies `pnSeed6_authorized` into the chain-parameter vector at offset `+0x260`, and `PeerAllowed()` reads that same vector before performing a membership search over converted peer addresses.

Separate disassembly shows `CConnman::OpenNetworkConnection()` invoking `PeerAllowed()` before continuing through the ordinary outbound connection path. A complete direct-call sweep also located `PeerAllowed()` in peer-eviction, address-message, block-message and compact-block processing paths.

The detailed forensic record is in [`HISTORICAL_NETWORK_CONTROL_EVIDENCE.md`](HISTORICAL_NETWORK_CONTROL_EVIDENCE.md).

## Revival decision

The revival SHALL NOT reproduce the historical requirement that ordinary peers must pass the operator-defined `PeerAllowed()` authorization test before establishing a normal outbound connection.

Revived AMLToken nodes use an ordinary peer-to-peer connection path. Compatible peers do not require membership in a privileged authorization table.

The historical authorization table is evidence only. It is not a permission list for the revival.

This is a network-availability change only.

It does NOT change:

- genesis;
- historical block hashes;
- proof of work;
- difficulty calculation;
- consensus validation;
- transaction validity;
- historical ownership;
- wallet keys;
- balances;
- historical chain data.

## Closed-network validation

A two-node test was performed in an isolated Linux network namespace with no external default route.

Both reconstructed nodes:

- used the recovered AMLToken mainnet genesis;
- connected as ordinary peers over loopback;
- completed protocol-version-70015 handshakes in both directions;
- exchanged standard P2P messages;
- required no `PeerAllowed()` or authorized-peer list;
- remained at block height 0;
- mined no blocks;
- touched no historical wallet;
- made no public network connection.

Evidence file:

```text
amlcore-peer-handshake-20260913_205259.txt
```

SHA-256:

```text
174b2764550ba6b9c9b8d8239aa8b5774b9a42f24cdd295b92ca3486d3ece3ab
```

## Current mainnet discovery baseline

A read-only audit of the reconstructed source confirmed the following **mainnet** state:

- default AMLToken P2P port: `23247`;
- no `PeerAllowed` symbol in the reconstructed source;
- no `pnSeed6_authorized` symbol in the reconstructed source;
- `vSeeds.clear()` for mainnet;
- `vFixedSeeds.clear()` for mainnet;
- ordinary manual peer connection support remains available through the inherited peer-to-peer connection path, including `-addnode`/`addnode` functionality.

Evidence file:

```text
amlcore-discovery-baseline-20260914_122106.txt
```

SHA-256:

```text
b4957187a8132bb0a2d82bc2b5d45df2081ebc877a07a82ef251071a885284e3
```

The empty mainnet seed lists are deliberate at this reconstruction stage. They prevent undocumented or guessed discovery infrastructure from being represented as historical fact.

## Non-mainnet warning

The current reconstruction work is authoritative only for the evidence-backed **mainnet** parameters documented in this repository.

The source tree still contains inherited upstream Bitcoin testnet configuration, including upstream Bitcoin testnet DNS/fixed seed material. That configuration has **not** been established as historical AMLToken testnet identity and must not be presented or used as such.

Until AMLToken-specific testnet evidence is recovered and reconstructed, operators should avoid using `-testnet` for AMLToken historical validation. Regtest may be useful for explicitly local engineering tests, but it is not historical mainnet evidence.

## Decentralized discovery policy

Historical seed infrastructure is preserved as forensic evidence, not reinstated as an authorization authority.

When revival discovery infrastructure is eventually introduced, the following rules apply:

1. Seed nodes provide discovery only. They do not determine which otherwise-valid peers may connect, relay, validate or participate.
2. No revival seed receives consensus, eviction, block-processing, address-processing or compact-block privileges merely because it is a seed.
3. Direct `-addnode`/`addnode` connections must remain possible without membership in any operator-controlled list.
4. Discovery should use multiple independently operated endpoints where practical rather than recreate a single administrative dependency.
5. Any new DNS or fixed seeds must be documented explicitly as **revival infrastructure**, not passed off as historical AMLToken data.
6. Historical endpoints recovered from the original binary must not be silently reactivated or treated as authoritative simply because they appeared in the 2018 software.
7. Public discovery infrastructure must not be activated as a substitute for recovering the legitimate historical chain.

This separates two questions that must remain distinct: **how peers discover one another** and **which blockchain history is legitimate**.

## Production restriction

The revival must not begin mining or extending a replacement production chain from genesis.

Production operation requires recovery or independent verification of the legitimate historical AMLToken chain tip.

Until then, networking tests must remain isolated or explicitly non-production. Revival seed deployment may be designed and tested, but it must not be used to manufacture a new production history from height 0.

---

**Same genesis. Same historical ledger. Same ownership. Decentralized peer access.**
