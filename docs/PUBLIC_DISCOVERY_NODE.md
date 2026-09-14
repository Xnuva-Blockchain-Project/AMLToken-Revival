# Public Historical-Chain Discovery Node

> Status: active as of 14 September 2026

A public AMLToken/ABTC recovery node is now available at:

```text
81.130.208.151:23247
```

## Purpose

This node exists solely to help locate and preserve the legitimate historical AMLToken/ABTC blockchain.

It is **not** a replacement production chain, a new token launch, a mining endpoint, or an authoritative substitute for the missing historical ledger.

The node is deliberately operated:

- without a wallet;
- without mining;
- with the recovered original AMLToken mainnet genesis;
- with ordinary peer connectivity rather than the historical operator-controlled authorization gate;
- with no invented post-genesis blocks, balances or ownership changes.

At the time this endpoint was published, the node remained at:

```text
blocks:  0
headers: 0
bestblockhash: 00000000230d6b389555e80e4523a32343531448ddd15fbc29c0fdc11dbb1538
```

That is intentional. The project will not manufacture replacement history merely to advance the chain.

## Connecting a surviving historical node

If you operate a surviving AMLToken node containing historical chain data, you may point it at the recovery endpoint using an ordinary addnode entry:

```text
addnode=81.130.208.151:23247
```

A compatible node that connects may advertise and relay historical headers and blocks. Any received chain data must still pass normal consensus validation before it can be treated as part of the recovered historical ledger.

Please preserve your existing data directory before making changes. Work from a copy where possible.

## Wallet and private-key safety

Do **not** publish or send:

- `wallet.dat`;
- private keys;
- seed phrases;
- wallet passphrases;
- `dumpwallet` or `dumpprivkey` output.

The recovery effort needs public blockchain history, not private wallet secrets.

Useful non-private material includes `blk*.dat`, block hashes, transaction IDs, public addresses, archived node data, old binaries and technical documentation.

## Reachability verification

The endpoint was externally tested from an independent Internet host on 14 September 2026. TCP connections to `81.130.208.151:23247` were accepted by the AMLToken discovery service.

The permanent node is configured to start automatically and remain available for historical-peer discovery.

## Recovery policy

If a historical peer supplies headers or blocks, the project will preserve the received data before analysis and will compare it against the recovered genesis, consensus parameters and independent historical evidence.

No received chain will be declared authoritative merely because it is longer or because a peer supplied it. Historical continuity and consensus validity must both be established.

See also:

- [`CHAIN_IDENTITY.md`](CHAIN_IDENTITY.md)
- [`GENESIS_REPRODUCTION.md`](GENESIS_REPRODUCTION.md)
- [`NETWORK_REVIVAL_POLICY.md`](NETWORK_REVIVAL_POLICY.md)
- [`RECONSTRUCTION_POLICY.md`](RECONSTRUCTION_POLICY.md)
- [`EVIDENCE_REGISTER.md`](EVIDENCE_REGISTER.md)

---

**Discovery is open. History is not being rewritten.**
