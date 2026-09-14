# AMLToken upstream baseline evidence

A major reconstruction lead has been identified from the preserved original AMLToken client build string.

This baseline work concerns the historical native **AMLToken/ABTC precursor chain**. It is not an attempt to reconstruct the later advertised AML Bitcoin system or its claimed proprietary biometric/AML/KYC features. See [`SCOPE_AND_TERMINOLOGY.md`](SCOPE_AND_TERMINOLOGY.md).

## Exact commit match

The original AMLToken-Qt v1.3.0 runtime reports:

```text
v1.3.0.0-ge278f86c5
```

The suffix `e278f86c5` resolves exactly to Bitcoin Core commit:

```text
e278f86c536921032e8288625dc5f3af610f2ec8
```

Commit date: **2017-09-16 05:40:45 UTC**.

Commit subject:

```text
Merge #11196: Switch memory_cleanse implementation to BoringSSL's to ensure memory clearing even with -lto
```

This makes that Bitcoin Core revision the strongest known upstream baseline candidate for reconstructing the vanished historical `AMLBitcoin/AMLCore` source used by the precursor-chain client.

## Runtime correlation

The same Bitcoin Core revision contains mainnet BIP9 deployment parameters matching those emitted by the original AMLToken client at height 0:

| Deployment | Bitcoin Core `e278f86c5` | AMLToken runtime |
| --- | ---: | ---: |
| CSV start | `1462060800` | `1462060800` |
| CSV timeout | `1493596800` | `1493596800` |
| SegWit start | `1479168000` | `1479168000` |
| SegWit timeout | `1510704000` | `1510704000` |

The Bitcoin revision also uses the same Bitcoin-Core-derived chain parameter structure, including `CMainParams`, BIP34/BIP65/BIP66 height fields, `powLimit`, target timespan/spacing, versionbits deployments, message-start bytes, default port, Base58 prefixes and `CreateGenesisBlock` construction.

## Interpretation

The exact build-hash match plus matching runtime deployment constants is strong evidence that AMLToken was derived from this Bitcoin Core source state or from a tree retaining this exact upstream revision marker.

It is **not proof that every unchanged AMLToken source file was byte-identical to Bitcoin Core at this commit**. AML-specific changes may have been committed, applied as patches, maintained outside the upstream history, or otherwise incorporated while retaining the upstream revision identifier.

Therefore reconstruction uses this commit as a **baseline candidate**, not as permission to assume all missing AMLToken parameters equal Bitcoin defaults.

## Reconstruction method

1. Preserve Bitcoin Core commit `e278f86c536921032e8288625dc5f3af610f2ec8` as the upstream reference tree.
2. Recover AML-specific differences from surviving original binaries, runtime RPC output, wallet/address behaviour and surviving historical block data.
3. Apply only evidence-backed AML-specific changes in the reconstruction branch.
4. Require deterministic reproduction of the original AMLToken genesis block and other verified fingerprints before accepting reconstructed source.
5. Do not inherit Bitcoin consensus constants merely because an AML value is not yet known.
6. Do not infer or import later advertised AML Bitcoin proprietary features into the recovered precursor-chain reconstruction.

**Same genesis. Same historical ledger. Same ownership.**