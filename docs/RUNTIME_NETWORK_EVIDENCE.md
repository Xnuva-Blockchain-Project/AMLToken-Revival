# AMLToken runtime network and consensus evidence

This document records read-only RPC output obtained from the preserved original **AMLToken-Qt v1.3.0** Windows client while it was running inside an operating-system network namespace with no external route.

The evidence fingerprints the historical native **AMLToken/ABTC precursor-chain client**. It does not establish or restore the later advertised AML Bitcoin system or its claimed proprietary features. See [`SCOPE_AND_TERMINOLOGY.md`](SCOPE_AND_TERMINOLOGY.md).

The client reported `connections: 0`. Its own `getnetworkinfo` flags still described IPv4 and IPv6 as reachable; those flags are application/runtime capability indicators and must not be interpreted as proof that the isolated process had Internet connectivity.

## `getnetworkinfo`

Verified runtime values:

| Field | Value |
| --- | --- |
| version | `1030000` |
| subversion | `/Satoshi:1.3.0/` |
| protocolversion | `70015` |
| localservices | `000000000000000d` |
| localrelay | `true` |
| timeoffset | `0` |
| networkactive | `true` |
| connections | `0` |
| relayfee | `0.00001000` |
| incrementalfee | `0.00001000` |
| localaddresses | empty |
| warnings | empty |

Network-family state reported by the client:

- IPv4: not limited, reachable, no proxy;
- IPv6: not limited, reachable, no proxy;
- onion: limited, not reachable, no proxy.

These values fingerprint the original runtime behaviour. They do not override the external isolation evidence from the host network namespace.

## `getblockchaininfo` at genesis-only state

The original client reported:

| Field | Value |
| --- | --- |
| chain | `main` |
| blocks | `0` |
| headers | `0` |
| bestblockhash | `00000000230d6b389555e80e4523a32343531448ddd15fbc29c0fdc11dbb1538` |
| difficulty | `1` |
| mediantime | `1505736000` |
| verificationprogress | `0` |
| chainwork | `0000000000000000000000000000000000000000000000000000000100010001` |
| pruned | `false` |

### Legacy softfork snapshot

At height 0 the client reported:

- BIP34 — version 2; reject status `false`;
- BIP66 — version 3; reject status `false`;
- BIP65 — version 4; reject status `false`.

### BIP9 snapshot

At height 0 the client reported:

- CSV — status `defined`, startTime `1462060800`, timeout `1493596800`, since `0`;
- SegWit — status `defined`, startTime `1479168000`, timeout `1510704000`, since `0`.

These are verified observations of the original client while only genesis was loaded. They must not be promoted into claims about later historical activation without surviving chain evidence or original consensus source.

## Reconstruction significance

A compatible revival node should reproduce these original runtime fingerprints where they reflect consensus or wire-protocol behaviour of the historical AMLToken/ABTC precursor chain. Cosmetic version strings may later be modernised, but historical block validation, network message compatibility and activation logic must be reconstructed from evidence rather than assumed from a modern Bitcoin release.

Any later functionality added by the revival must be labelled as forward revival-era engineering and must not be described as proof that the later advertised AML Bitcoin system possessed that functionality historically.

**Same genesis. Same historical ledger. Same ownership.**