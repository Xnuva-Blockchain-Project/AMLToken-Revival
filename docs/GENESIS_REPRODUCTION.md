# AMLToken genesis reproduction

This document records a deterministic reproduction of the original AMLToken mainnet genesis block header hash using runtime metadata obtained from the preserved 2018 AMLToken client.

## Runtime inputs

| Field | Value |
| --- | --- |
| version | `1` |
| previous block hash | 32 zero bytes |
| merkle root | `86f66413faa11cb678541c8b635a42845cefe9951ed528fb20e0306be22500d2` |
| time | `1505736000` |
| bits | `1d00ffff` |
| nonce | `676078011` (`0x284c21bb`) |

## Serialized 80-byte header

Using standard Bitcoin block-header serialization — little-endian integer fields and internal little-endian hash byte order — the exact header is:

```text
010000000000000000000000000000000000000000000000000000000000000000000000d20025e26b30e020fb28d51e95e9ef5c84425a638b1c5478b61ca1fa1364f68640b5bf59ffff001dbb214c28
```

Length: **80 bytes**.

## Hash reproduction

Applying standard Bitcoin double SHA-256 to those 80 bytes and reversing the resulting digest for conventional display produces:

```text
00000000230d6b389555e80e4523a32343531448ddd15fbc29c0fdc11dbb1538
```

This exactly matches `getblockhash 0` and the `hash` field returned by `getblock` from the original AMLToken-Qt v1.3.0 client.

Therefore the original AMLToken **block identifier / `CBlockHeader::GetHash()` behaviour is verified as standard Bitcoin SHA-256d for the genesis header**.

## Proof-of-work caution

This result proves the block-header identifier hash. It is very strong evidence for Bitcoin-style SHA-256d Proof of Work, especially because static inspection has not revealed a separate `GetPoWHash` or scrypt path. However, the project will keep the broader production PoW algorithm formally pending until the historical proof-of-work validation path is independently identified or reproduced.

No consensus parameter should be changed merely to make mining convenient.

**Same genesis. Same historical ledger. Same ownership.**
