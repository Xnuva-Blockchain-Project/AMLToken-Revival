# AMLToken mining evidence

This document records mining-related behaviour observed directly from the preserved original **AMLToken-Qt v1.3.0** client. It is an evidence record, not a redesign specification.

The evidence concerns the historical native **AMLToken/ABTC precursor chain**. It does not establish or restore the later advertised AML Bitcoin system or any claimed proprietary biometric/AML/KYC functionality. See [`SCOPE_AND_TERMINOLOGY.md`](SCOPE_AND_TERMINOLOGY.md).

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

The spelling above is preserved exactly as emitted by the original client. This result means the client refuses to provide a mining template while it considers itself disconnected. The genesis-only isolated session therefore did not reveal the historical next-block candidate parameters through `getblocktemplate`; those rules were later recovered from binary analysis and validated against historical block data where applicable.

This connectivity requirement was not bypassed by weakening consensus code.

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

## Original Proof-of-Work validation path

A focused static audit of the preserved original Linux `AMLToken-Qt` binary identified these exported consensus functions:

```text
GetNextWorkRequired(CBlockIndex const*, CBlockHeader const*, Consensus::Params const&)
CalculateNextWorkRequired(CBlockIndex const*, long, Consensus::Params const&)
CheckProofOfWork(uint256, unsigned int, Consensus::Params const&)
```

The original binary also exposes `CBlockHeader::GetHash() const`, which dispatches through `SerializeHash<CBlockHeader>`. No separate `GetPoWHash`, scrypt, X11, or other alternate block-work hash path was found in the symbol audit.

The focused disassembly evidence was stored locally as `amltoken-pow-focused.txt`; its SHA-256 is:

```text
1b66ff6b8286590c205c38dfe51182487846e196b91cad1b28a4667904b8fbf7
```

### Difficulty selection

`GetNextWorkRequired` in the original binary:

- converts `powLimit` to compact form;
- computes the difficulty interval from `nPowTargetTimespan / nPowTargetSpacing`;
- returns the prior block difficulty outside adjustment boundaries;
- retains the Bitcoin-style optional minimum-difficulty test-chain rule;
- walks back through prior minimum-difficulty blocks under that rule;
- at an adjustment boundary, selects the first block of the interval and calls `CalculateNextWorkRequired`;
- respects `fPowNoRetargeting`.

With the recovered AMLToken mainnet parameters `nPowTargetTimespan = 600` seconds and `nPowTargetSpacing = 60` seconds, the mainnet difficulty-adjustment interval is **10 blocks**.

### Retarget calculation

`CalculateNextWorkRequired` in the original binary reproduces the standard Bitcoin-Core retarget formula:

1. `actualTimespan = lastBlockTime - firstBlockTime`;
2. clamp actual timespan to `[targetTimespan / 4, targetTimespan * 4]`;
3. decode the previous compact target;
4. multiply by the clamped actual timespan;
5. divide by the target timespan;
6. cap the result at `powLimit`;
7. return the compact target.

No alternate retarget formula was observed.

### Proof validation

`CheckProofOfWork` in the original binary reproduces the standard Bitcoin-Core checks:

- decode `nBits` with compact-target negative/overflow flags;
- reject negative, zero, overflowed, or above-`powLimit` targets;
- convert the supplied 256-bit block hash to arithmetic form;
- accept only when `hash <= target`.

Combined with the verified `CBlockHeader::GetHash()` SHA-256d behaviour and successful full reindexes of the recovered historical block data, this establishes the historical AMLToken/ABTC precursor-chain Proof-of-Work path as **Bitcoin-style SHA-256d Proof of Work with the recovered Bitcoin-Core-style difficulty algorithm**.

Accordingly, the reconstruction should leave upstream `pow.cpp` unchanged unless later surviving historical blocks provide contradictory evidence.

## Preservation requirement

Mining must not begin on a replacement history from block 1. The project has authenticated the AMLToken/ABTC precursor ledger through height **175168**, but that height is not claimed as the final historical tip.

Any future production continuation must extend the genuine authenticated historical tip once that boundary is established. Development mining may be performed only on clearly labelled isolated test chains or regression environments and must never be represented as historical AMLToken mainnet history or as proof of later advertised AML Bitcoin capabilities.

**Same genesis. Same historical ledger. Same ownership.**