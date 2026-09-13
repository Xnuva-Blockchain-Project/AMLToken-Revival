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

Separate disassembly shows `CConnman::OpenNetworkConnection()` invoking `PeerAllowed()` before continuing through the ordinary outbound connection path.

The detailed forensic record is in [`HISTORICAL_NETWORK_CONTROL_EVIDENCE.md`](HISTORICAL_NETWORK_CONTROL_EVIDENCE.md).

## Revival decision

The revival SHALL NOT reproduce the historical requirement that ordinary peers must pass the operator-defined `PeerAllowed()` authorization test before establishing a normal outbound connection.

Revived AMLToken nodes use an ordinary peer-to-peer connection path. Compatible peers do not require membership in a privileged authorization table.

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

## Seed policy

Historical seed infrastructure is preserved as forensic evidence, not reinstated as an authorization authority.

Future revival seed nodes may be introduced as clearly documented discovery infrastructure. Seed operators must not receive consensus privileges or the ability to determine which otherwise-valid peers are permitted to participate.

Direct `-addnode` connections and ordinary peer discovery must remain possible.

## Production restriction

The revival must not begin mining or extending a replacement production chain from genesis.

Production operation requires recovery or independent verification of the legitimate historical AMLToken chain tip.

Until then, networking tests must remain isolated or explicitly non-production.

---

**Same genesis. Same historical ledger. Same ownership. Decentralized peer access.**
