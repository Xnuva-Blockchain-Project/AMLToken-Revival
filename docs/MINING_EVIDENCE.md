# AMLToken mining evidence

This document records mining-related behaviour observed directly from the preserved original **AMLToken-Qt v1.3.0** client. It is an evidence record, not a redesign specification.

## Observed client state

The original client was started against an isolated data directory with no external network connectivity. At genesis-only state it reported:

```text
blocks: 0
currentblockweight: 0
currentblocktx: 0
difficulty: 1
networkhashps: 0
pooledtx: 0
chain: main
```

This establishes that the historical AMLToken software exposes Bitcoin-Core-style Proof-of-Work mining state through `getmininginfo`.

## External miner interface

`help getblocktemplate` is present in the original client. The help describes the BIP 22/23 block-template interface and reports fields including:

- `previousblockhash`
- `transactions`
- `coinbasevalue`
- `target`
- `noncerange`
- `bits`
- `height`
- `curtime`

This establishes that external mining software was expected to obtain candidate block templates from the AMLToken node using the standard Bitcoin-Core-derived mining RPC model.

When `getblocktemplate` was invoked while the original client was deliberately isolated from all peers, it returned:

```text
ALMToken is not connected! (code -9)
```

The spelling above is preserved exactly as emitted by the original client. This result means the client refuses to provide a mining template while it considers itself disconnected. Therefore the genesis-only isolated session cannot yet reveal the historical next-block coinbase reward, target or candidate-block parameters through `getblocktemplate`.

This connectivity requirement must not be bypassed by altering consensus code merely to obtain a template. A controlled test network can be used later once compatible reconstructed nodes exist.

## Solved-block submission

`help submitblock` is also present. The original client documents:

```text
submitblock "hexdata"  ( "dummy" )
```

and states that the RPC attempts to submit a new block to the network using the BIP 22 model. The second compatibility argument is ignored.

Together, `getblocktemplate` and `submitblock` establish the expected external-miner workflow: obtain a template from the node, construct and solve a candidate block externally, then return the complete serialized block to the node for validation and acceptance.

## Built-in CPU generation

`help setgenerate` returns:

```text
help: unknown command: setgenerate
```

Therefore AMLToken-Qt v1.3.0 does not expose the old wallet-integrated `setgenerate` CPU-mining RPC. Revival mining should not depend on adding such a facility merely for convenience.

## Header hash verification

The original client's runtime genesis metadata was serialized as a standard 80-byte Bitcoin-style block header and hashed with double SHA-256. The resulting displayed hash is exactly:

```text
00000000230d6b389555e80e4523a32343531448ddd15fbc29c0fdc11dbb1538
```

which matches the original client's `getblockhash 0` and `getblock` results byte-for-byte. The complete deterministic reproduction is recorded in [`GENESIS_REPRODUCTION.md`](GENESIS_REPRODUCTION.md).

Therefore **AMLToken block identifiers / `CBlockHeader::GetHash()` are verified to use standard Bitcoin SHA-256d for the genesis header**.

## PoW algorithm status

The broader production Proof-of-Work validation algorithm remains formally **pending**, rather than being guessed. The verified SHA-256d block-header hash, Bitcoin-derived `getblocktemplate`/`submitblock` interfaces, difficulty-one genesis, and absence so far of a separate `GetPoWHash` or scrypt identifier are strong evidence for Bitcoin-style SHA-256d Proof of Work.

However, some historical altcoins used a standard SHA-256d block identifier while validating work with a separate PoW hash. Before revival mainnet mining is enabled, the proof-of-work validation path must therefore be independently identified from original source/binary logic or reproduced against surviving historical blocks.

## Preservation requirement

Mining must not begin on a replacement history from block 1. The revival objective is to recover and validate the historical AMLToken ledger and then, if continuity can be established, extend that same chain from its legitimate historical tip.

Development mining may be performed only on clearly labelled isolated test chains or regression environments and must never be represented as historical AMLToken mainnet history.

**Same genesis. Same historical ledger. Same ownership.**