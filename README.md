# AMLToken Revival

AMLToken Revival is an independent preservation and recovery project for the original **AMLToken (ABTC)** blockchain.

## Why this project exists

The original AMLToken / AML Bitcoin operation ceased to provide a practical path for some historical purchasers and token holders to access, verify, or convert their holdings. Subsequent criminal fraud proceedings involving the original operation reinforced the need to preserve the technical record independently.

This project exists to help protect affected historical holders by preserving the original blockchain evidence and, where technically possible, restoring access to the original network without rewriting ownership.

This is **not a new token launch** and it is not an attempt to create replacement balances for old holders.

## Preservation rule

**Same genesis. Same historical ledger. Same ownership.**

The project will not:

- create a replacement genesis block;
- arbitrarily issue coins or recreate balances by hand;
- rewrite legitimate historical transactions;
- require holders to surrender private keys in order to establish ownership;
- present a reconstructed chain as original unless its historical continuity can be demonstrated.

Any unavoidable forward-only repair or modernisation must be documented and must not retroactively alter legitimate historical ownership.

## Recovery objective

The immediate objective is to reconstruct enough of the original AMLToken Core software and chain parameters to reproduce the historical network exactly, beginning with the known original mainnet genesis block:

```text
00000000230d6b389555e80e4523a32343531448ddd15fbc29c0fdc11dbb1538
```

From there, the project will attempt to locate or reconstruct surviving historical blockchain data, validate original transactions, and determine whether the original ledger can be brought back into service without creating a new chain.

## Historical network-control finding

Static analysis of the preserved original AMLToken-Qt v1.3.0 Linux client has established that the historical software contained a separate **authorized-peer table** and an active `PeerAllowed()` membership check used in the outbound connection path.

The original mainnet constructor loaded both a normal 13-entry seed table and a separate 13-entry authorized table. The two tables contained essentially the same endpoint set. This created a dependency on a small operator-defined peer infrastructure for normal outbound connectivity.

The revival does **not** reproduce that centralized peer-authorization requirement. This networking repair is documented separately from consensus reconstruction and does not authorize any change to genesis, historical transactions, balances or ownership.

Full technical evidence:

- [`docs/HISTORICAL_NETWORK_CONTROL_EVIDENCE.md`](docs/HISTORICAL_NETWORK_CONTROL_EVIDENCE.md) — recovered authorized-peer tables, `PeerAllowed()` disassembly and mainnet constructor mapping;
- [`docs/NETWORK_REVIVAL_POLICY.md`](docs/NETWORK_REVIVAL_POLICY.md) — why the revival removes the historical peer gate while preserving the original ledger and consensus identity.

The evidence establishes the mechanism and its effect on connectivity. It does not attempt to infer developer motive beyond what the preserved binary proves.

## Reconstruction records

Work on the `reconstruction` branch is evidence-led. The current records are:

- [`docs/CHAIN_IDENTITY.md`](docs/CHAIN_IDENTITY.md) — verified chain identity and parameters recovered from original software;
- [`docs/GENESIS_REPRODUCTION.md`](docs/GENESIS_REPRODUCTION.md) — byte-level genesis reconstruction and deterministic hash reproduction;
- [`docs/EVIDENCE_REGISTER.md`](docs/EVIDENCE_REGISTER.md) — provenance and evidence status for preserved artefacts;
- [`docs/MINING_EVIDENCE.md`](docs/MINING_EVIDENCE.md) — mining RPC behaviour and what remains unverified;
- [`docs/RUNTIME_NETWORK_EVIDENCE.md`](docs/RUNTIME_NETWORK_EVIDENCE.md) — original protocol, network and consensus-deployment runtime fingerprints;
- [`docs/HISTORICAL_NETWORK_CONTROL_EVIDENCE.md`](docs/HISTORICAL_NETWORK_CONTROL_EVIDENCE.md) — evidence of the historical authorized-peer access-control mechanism;
- [`docs/NETWORK_REVIVAL_POLICY.md`](docs/NETWORK_REVIVAL_POLICY.md) — decentralized connectivity policy for the revival;
- [`docs/UPSTREAM_BASELINE.md`](docs/UPSTREAM_BASELINE.md) — evidence identifying the strongest known Bitcoin Core upstream baseline candidate;
- [`docs/RECONSTRUCTION_POLICY.md`](docs/RECONSTRUCTION_POLICY.md) — holder-protection and consensus-continuity rules.

Values that have not been established from surviving evidence are left unknown rather than guessed.

## Holder safety

Historical holders should **never publish or submit** wallet files, private keys, seed phrases, wallet passphrases, or private-key dumps.

Public addresses, transaction IDs, block hashes and other public blockchain data may be used as evidence. Where ownership needs to be demonstrated, the preferred approach is cryptographic proof that does not expose private key material.

## Independence

AMLToken Revival is an independent preservation project. It is **not affiliated with, endorsed by, or operated by** the original AMLToken, AML Bitcoin, NAC Foundation, or their former operators.

## Current status

The repository is currently private while the original chain parameters, software behaviour and historical evidence are being reconstructed and verified. No public release or replacement network should be considered authoritative until the original chain identity and consensus behaviour have been reproduced and independently checked.
