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

This establishes that external mining software was expected to obtain candidate block templates from the AMLToken node and submit work using the standard Bitcoin-Core-derived mining RPC model.

When `getblocktemplate` was invoked while the original client was deliberately isolated from all peers, it returned:

```text
ALMToken is not connected! (code -9)
```

The spelling above is preserved exactly as emitted by the original client. This result means the client refuses to provide a mining template while it considers itself disconnected. Therefore the genesis-only isolated session cannot yet reveal the historical next-block coinbase reward, target or candidate-block parameters through `getblocktemplate`.

This connectivity requirement must not be bypassed by altering consensus code merely to obtain a template. A controlled test network can be used later once compatible reconstructed nodes exist.

## Built-in CPU generation

`help setgenerate` returns:

```text
help: unknown command: setgenerate
```

Therefore AMLToken-Qt v1.3.0 does not expose the old wallet-integrated `setgenerate` CPU-mining RPC. Revival mining should not depend on adding such a facility merely for convenience.

## PoW algorithm status

The precise Proof-of-Work hash algorithm is **not yet marked verified** in this project. The binary uses `CBlockHeader::GetHash()` and no `scrypt` or `GetPoWHash` identifier has yet been found in the recovered static evidence, which is consistent with the Bitcoin-Core-derived implementation but is not, by itself, sufficient proof that the production PoW is SHA-256d.

The algorithm must be established from original source, deterministic binary analysis, or an independently reproduced header/hash test before revival mining is enabled.

## Preservation requirement

Mining must not begin on a replacement history from block 1. The revival objective is to recover and validate the historical AMLToken ledger and then, if continuity can be established, extend that same chain from its legitimate historical tip.

Development mining may be performed only on clearly labelled isolated test chains or regression environments and must never be represented as historical AMLToken mainnet history.

**Same genesis. Same historical ledger. Same ownership.**
