# AMLToken genesis reproduction

This document records a deterministic reproduction of the original AMLToken mainnet genesis block using runtime data obtained from the preserved 2018 AMLToken client.

## Runtime inputs

| Field | Value |
| --- | --- |
| version | `1` |
| previous block hash | 32 zero bytes |
| merkle root | `86f66413faa11cb678541c8b635a42845cefe9951ed528fb20e0306be22500d2` |
| time | `1505736000` |
| bits | `1d00ffff` |
| nonce | `676078011` (`0x284c21bb`) |
| serialized block size | `281` bytes |
| transaction count | `1` |

## Serialized 80-byte header

Using standard Bitcoin block-header serialization — little-endian integer fields and internal little-endian hash byte order — the exact header is:

```text
010000000000000000000000000000000000000000000000000000000000000000000000d20025e26b30e020fb28d51e95e9ef5c84425a638b1c5478b61ca1fa1364f68640b5bf59ffff001dbb214c28
```

Length: **80 bytes**.

Applying standard Bitcoin double SHA-256 to those 80 bytes and reversing the digest for conventional display produces:

```text
00000000230d6b389555e80e4523a32343531448ddd15fbc29c0fdc11dbb1538
```

This exactly matches `getblockhash 0` and the `hash` field returned by `getblock` from the original AMLToken-Qt v1.3.0 client.

Therefore the original AMLToken **block identifier / `CBlockHeader::GetHash()` behaviour is verified as standard Bitcoin SHA-256d for the genesis header**.

## Raw genesis block

The original client returned the complete genesis block with `getblock <genesis-hash> false`:

```text
010000000000000000000000000000000000000000000000000000000000000000000000d20025e26b30e020fb28d51e95e9ef5c84425a638b1c5478b61ca1fa1364f68640b5bf59ffff001dbb214c280101000000010000000000000000000000000000000000000000000000000000000000000000ffffffff4904ffff001d0104415468652054696d65732031382f5365702f3230313720476f6f676c65204a6f696e7320496e646961277320636173686c657373207061796d656e74732072757368ffffffff016400000000000000434104678afdb0fe5548271967f1a67130b7105cd6a828e03909a67962e0ea1f61deb649f6bc3f4cef38c4f35504e51ec112de5c384df7ba0b8d578a4c702b6bf11d5fac00000000
```

Its length is exactly **281 bytes**, matching the original client's `size` and `strippedsize` values.

## Genesis transaction

The block contains one 200-byte transaction:

```text
01000000010000000000000000000000000000000000000000000000000000000000000000ffffffff4904ffff001d0104415468652054696d65732031382f5365702f3230313720476f6f676c65204a6f696e7320496e646961277320636173686c657373207061796d656e74732072757368ffffffff016400000000000000434104678afdb0fe5548271967f1a67130b7105cd6a828e03909a67962e0ea1f61deb649f6bc3f4cef38c4f35504e51ec112de5c384df7ba0b8d578a4c702b6bf11d5fac00000000
```

Double-SHA256 of the serialized transaction gives:

```text
86f66413faa11cb678541c8b635a42845cefe9951ed528fb20e0306be22500d2
```

With only one transaction in the block, that transaction ID is also the genesis merkle root, exactly matching the value reported by the original client.

The coinbase transaction decodes structurally as:

- transaction version: `1`
- one coinbase input, null previous hash and index `0xffffffff`
- coinbase script length: `73` bytes
- sequence: `0xffffffff`
- one output
- serialized output value: integer `100` base units
- output script length: `67` bytes
- output script: 65-byte uncompressed public key followed by `OP_CHECKSIG`
- locktime: `0`

The coinbase script contains the exact 65-byte historical message:

```text
The Times 18/Sep/2017 Google Joins India's cashless payments rush
```

The serialized integer output value is recorded as **100 base units** only. Its human-readable ABTC denomination should not be inferred until the historical monetary-unit constant is independently verified.

## Proof-of-work caution

This result proves the block-header identifier hash. It is very strong evidence for Bitcoin-style SHA-256d Proof of Work, especially because static inspection has not revealed a separate `GetPoWHash` or scrypt path. However, the project will keep the broader production PoW algorithm formally pending until the historical proof-of-work validation path is independently identified or reproduced.

No consensus parameter should be changed merely to make mining convenient.

**Same genesis. Same historical ledger. Same ownership.**
