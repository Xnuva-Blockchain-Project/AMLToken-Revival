# AMLToken (ABTC) — Chain Identity Record

This document records chain-identity facts recovered from surviving original AMLToken software. It is deliberately conservative: observations are separated from values recovered by static analysis, and uncertain values are not promoted to consensus facts.

## Preservation invariant

**Same genesis. Same historical ledger. Same ownership.**

A revived implementation is not considered compatible merely because it uses the AMLToken name or ABTC ticker. It must reproduce the original chain identity and consensus behaviour.

## Runtime-verified identity

The following values were obtained directly from the original 2018 `AMLToken-Qt v1.3.0` Windows client while it was run in an isolated, network-disabled environment.

| Property | Value | Status |
| --- | --- | --- |
| Currency / ticker | ABTC | VERIFIED |
| Client | AMLToken-Qt v1.3.0 | VERIFIED |
| Reported build | v1.3.0.0-ge278f86c5 (64-bit) | VERIFIED |
| Runtime version | `1030000` | VERIFIED |
| P2P protocol version | `70015` | VERIFIED |
| Subversion string | `/Satoshi:1.3.0/` | VERIFIED |
| Local services | `000000000000000d` | VERIFIED |
| Mainnet genesis block hash | `00000000230d6b389555e80e4523a32343531448ddd15fbc29c0fdc11dbb1538` | VERIFIED |
| Genesis height | `0` | VERIFIED |
| Genesis version | `1` (`00000001`) | VERIFIED |
| Genesis timestamp (`nTime`) | `1505736000` | VERIFIED |
| Genesis UTC time | 2017-09-18 12:00:00 UTC | VERIFIED / derived from runtime timestamp |
| Genesis nonce (`nNonce`) | `676078011` (`0x284c21bb`) | VERIFIED |
| Genesis difficulty bits (`nBits`) | `1d00ffff` | VERIFIED |
| Genesis difficulty | `1` | VERIFIED |
| Genesis merkle root | `86f66413faa11cb678541c8b635a42845cefe9951ed528fb20e0306be22500d2` | VERIFIED |
| Genesis transaction ID | `86f66413faa11cb678541c8b635a42845cefe9951ed528fb20e0306be22500d2` | VERIFIED |
| Genesis stripped size | `281` bytes | VERIFIED |
| Genesis serialized size | `281` bytes | VERIFIED |
| Genesis weight | `1124` | VERIFIED |
| Genesis chainwork | `0000000000000000000000000000000000000000000000000000000100010001` | VERIFIED |

A clean isolated datadir reported `getblockcount = 0`, and `getblockhash 0` returned the genesis hash above. `getblock <genesis-hash>` independently returned the runtime metadata recorded in this table.

The equality of the genesis transaction ID and merkle root is expected for a block containing exactly one transaction and is directly reported by the original client.

## Runtime consensus-deployment snapshot at height 0

`getblockchaininfo` on the original client reported the following state while only genesis was present:

| Deployment | Runtime state at height 0 |
| --- | --- |
| BIP34 | version 2; reject status `false` |
| BIP66 | version 3; reject status `false` |
| BIP65 | version 4; reject status `false` |
| CSV | BIP9 status `defined`; startTime `1462060800`; timeout `1493596800`; since `0` |
| SegWit | BIP9 status `defined`; startTime `1479168000`; timeout `1510704000`; since `0` |

These values are a verified snapshot of the original client's state at height 0. They do **not** by themselves establish which deployments later activated on the historical AMLToken chain; that must be determined from original consensus parameters and/or surviving historical blocks.

## Values recovered from original binary analysis

The following mainnet values have now been recovered directly from the original Linux AMLToken binary's `CMainParams` constructor and adjacent read-only constant data.

| Property | Value | Evidence state |
| --- | --- | --- |
| Subsidy-halving interval | `800000` | EXTRACTED |
| BIP34 height | `227931` | EXTRACTED; same numeric height as upstream baseline |
| BIP34 hash | zero / `0x00` | EXTRACTED |
| BIP65 height | `388381` | EXTRACTED; same numeric height as upstream baseline |
| BIP66 height | `363725` | EXTRACTED; same numeric height as upstream baseline |
| PoW limit | `00000000ffffffffffffffffffffffffffffffffffffffffffffffffffffffff` | EXTRACTED |
| PoW target spacing | `60` seconds | EXTRACTED |
| PoW target timespan | `600` seconds | EXTRACTED |
| Allow minimum-difficulty blocks | `false` | EXTRACTED |
| Disable retargeting | `false` | EXTRACTED |
| BIP9 activation threshold | `1916` | EXTRACTED |
| BIP9 confirmation window | `2016` | EXTRACTED |
| Minimum chain work | zero / `0x00` | EXTRACTED |
| Default assume-valid | zero / `0x00` | EXTRACTED |
| Mainnet message start / magic | `0d 1c 81 52` | EXTRACTED — runtime/network confirmation still required |
| Default mainnet P2P port | `23247` / `0x5acf` | EXTRACTED — runtime/network confirmation still required |
| Prune-after height | `100000` | EXTRACTED |
| P2PKH / `PUBKEY_ADDRESS` prefix | `0x41` / decimal `65` | EXTRACTED; independently consistent with recovered historical AMLToken address |
| P2SH / `SCRIPT_ADDRESS` prefix | `0x05` | EXTRACTED |
| WIF / `SECRET_KEY` prefix | `0xc1` / decimal `193` | EXTRACTED |
| Extended private-key prefix | `04 88 ad e4` | EXTRACTED |
| Extended public-key prefix | `04 88 b2 1e` | EXTRACTED |

The original static extraction also produced `nTime = 0x59bfb540`, `nNonce = 0x284c21bb`, and `nBits = 0x1d00ffff`. Those three values are independently confirmed by the running original client and have therefore been promoted to **VERIFIED** above.

The HD-key constants were recovered from the exact byte ranges used by the mainnet constructor: the constructor copies bytes `04 88 b2 1e` into the extended-public-key vector and `04 88 ad e4` into the extended-secret-key vector. They are therefore not inferred from Bitcoin defaults merely because the upstream baseline used the same values.

## Original software fingerprints

These hashes identify preserved original artefacts used during recovery. They are evidence fingerprints, not replacement binaries.

| Artefact | SHA-256 |
| --- | --- |
| `AMLToken-Qt-1.3.0.exe` | `39cc74896e0fc6ebf313fe8a880be6f74466f8f4314fdff889a73053c23297dd` |
| `AMLToken-Qt-1.3.0-Win10x64.zip` | `476036079d4999124ac1e120ec400589d012a907abfb38c072930e7ef9669abb` |
| Linux `AMLToken-Qt` binary | `61c61988ef5e672ab3aeaa2dba9410f161907433a96c0755cd6484e78d6089d4` |

The Windows executable contains Berkeley DB 4.8.30 support and identifies itself as AMLToken/AML Token software. Static strings and source paths point to the historical `AMLBitcoin/AMLCore` codebase.

## Important distinction

The historical C++ AMLToken/ABTC chain documented here is distinct from the later Go/Skycoin-derived AML Bitcoin codebase found under `amltoken/amltoken`. The latter must not be used as a substitute genesis or ledger for ABTC holders.

## Acceptance gate for reconstruction

Before reconstructed source is treated as an AMLToken-compatible node, it must at minimum:

1. deterministically reproduce the exact mainnet genesis hash above;
2. reproduce the exact genesis transaction and merkle root;
3. reproduce the original address/network encoding and message-start bytes;
4. reproduce historical consensus rules for all known pre-revival heights;
5. accept original serialized transactions and blocks without rewriting them;
6. preserve existing private-key ownership and historical balances;
7. avoid any new genesis, premine, manual balance allocation or synthetic migration ledger.

Values marked **EXTRACTED** remain evidence to verify, not permission to guess missing consensus parameters.