# Historical AMLToken network-control evidence

This document records evidence recovered from the preserved original **AMLToken-Qt v1.3.0** Linux binary showing that the historical client contained an operator-defined peer authorization mechanism in addition to ordinary fixed-seed infrastructure.

The purpose of publishing this material is transparency. It documents what the original software actually did, what users depended on for connectivity, and why the revival deliberately does not restore a centralized peer-authorization gate.

This document describes technical behaviour only. It does **not** attempt to infer the developers' motive or intent beyond what the binary proves.

## Source artefact

Preserved original Linux executable:

- file: `AMLToken-Qt`
- SHA-256: `61c61988ef5e672ab3aeaa2dba9410f161907433a96c0755cd6484e78d6089d4`
- historical version family: AMLToken v1.3.0
- analysis method: static ELF, symbol, DWARF and disassembly analysis; the executable was not connected to the Internet during this work

## Two separate historical seed tables

The original binary contains two named arrays:

```text
pnSeed6_authorized
pnSeed6_main
```

The ELF symbol table identifies both as 260-byte objects:

```text
0000000000cac140 0000000000000104 d pnSeed6_authorized
0000000000cac260 0000000000000104 d pnSeed6_main
```

Debug information identifies each as:

```cpp
SeedSpec6[13]
```

The AMLToken build modified the upstream Bitcoin `SeedSpec6` structure by adding a `mask` field:

```cpp
struct SeedSpec6 {
    uint8_t  addr[16];
    uint16_t port;
    uint16_t mask;
};
```

The original debug information reports a total size of 20 bytes per record, giving exactly 13 entries in each 260-byte table.

This differs from the upstream Bitcoin Core baseline structure, which contained only the 16-byte address and 16-bit port.

## Recovered endpoint set

Both historical tables contain the same 13 IPv4-mapped addresses:

| # | Address | `pnSeed6_authorized` port | `pnSeed6_main` port | mask |
| ---: | --- | ---: | ---: | ---: |
| 1 | `35.166.31.231` | `23247` | `23237` | `128` |
| 2 | `34.210.82.142` | `23247` | `23247` | `128` |
| 3 | `35.166.163.166` | `23247` | `23247` | `128` |
| 4 | `52.35.206.162` | `23247` | `23247` | `128` |
| 5 | `52.89.158.55` | `23247` | `23247` | `128` |
| 6 | `34.212.85.116` | `23247` | `23247` | `128` |
| 7 | `52.40.229.23` | `23247` | `23247` | `128` |
| 8 | `54.193.112.237` | `23247` | `23247` | `128` |
| 9 | `54.67.56.68` | `23247` | `23247` | `128` |
| 10 | `13.57.35.119` | `23247` | `23247` | `128` |
| 11 | `52.200.192.147` | `23247` | `23247` | `128` |
| 12 | `54.242.29.87` | `23247` | `23247` | `128` |
| 13 | `18.221.141.153` | `23247` | `23247` | `128` |

The first `pnSeed6_main` record differs only in port (`23237` rather than `23247`). The significance of that one-port difference remains under investigation and is not guessed here.

## `PeerAllowed()` is a real authorization check

The original binary exports:

```text
PeerAllowed(CAddress const&, CChainParams const&)
```

Its disassembly shows that it:

1. advances from the supplied `CChainParams` object to offset `+0x260`;
2. passes that vector to `convertSeed6(...)`;
3. searches the resulting `std::vector<CAddress>` for the supplied peer address;
4. returns true when the peer is found and false when it is not.

The relevant logic is therefore a membership test, not merely a descriptive label.

## The authorized table is the vector used by `PeerAllowed()`

The main-network constructor provides the missing layout proof.

`CMainParams::CMainParams()` copies `pnSeed6_main` into the chain-parameter vector at offset `+0x248`.

Immediately afterwards it copies `pnSeed6_authorized` into the vector at offset `+0x260`.

`PeerAllowed()` itself adds `0x260` to the `CChainParams` pointer before calling `convertSeed6()`.

This establishes that the list consulted by `PeerAllowed()` is the historical `pnSeed6_authorized` table.

## Connection-path effect

Separate disassembly of `CConnman::OpenNetworkConnection(...)` shows the historical AMLToken client calling `PeerAllowed()` before continuing through its normal outbound connection path.

The result is used as a branch condition. An allowed peer continues through the permitted path; a peer that does not satisfy the check follows the rejection/non-normal path.

Additional calls to `PeerAllowed()` exist in peer-eviction and message-processing paths. These additional uses mean it would be unsafe to revive the network by changing `PeerAllowed()` to always return true: doing so could grant all peers special treatment that the original software reserved for entries in the authorized list.

The evidence currently establishes an **outbound peer authorization gate**. It should not be overstated as proof that every inbound TCP connection was rejected directly at `AcceptConnection()`; that specific claim has not been established.

## Why this mattered to holders

The historical software therefore depended on a small, explicitly defined authorized-peer set for normal outbound connectivity.

Because the ordinary fixed-seed table and the authorized table contain essentially the same 13 addresses, loss or shutdown of that infrastructure could leave a normal wallet unable to establish the expected peer connections even though its wallet file, private keys and historical transaction records remained intact.

This provides a technically plausible explanation for historical clients remaining at states such as `Connecting to peers...` after the original infrastructure disappeared.

It does **not**, by itself, prove that this mechanism was the sole reason the historical network ceased to function.

## Revival policy

AMLToken Revival will not reproduce the historical requirement that an ordinary peer must belong to an operator-controlled authorized list before it can use the normal outbound connection path.

The reconstructed node retains ordinary decentralized peer connectivity while preserving chain-critical identity and validation rules.

The revival does **not** use removal of this network gate as permission to alter:

- the original genesis block;
- historical block hashes;
- proof-of-work validation;
- difficulty rules;
- historical transactions;
- balances;
- wallet ownership;
- private-key ownership;
- legitimate historical chain data.

No replacement production chain is to be mined from genesis while the legitimate historical post-genesis chain remains unrecovered.

## Closed-network validation of the revival decision

Two reconstructed AMLToken nodes were started in an isolated Linux network namespace with no external default route.

Both nodes used the exact recovered AMLToken genesis:

```text
00000000230d6b389555e80e4523a32343531448ddd15fbc29c0fdc11dbb1538
```

An ordinary direct peer connection completed a full two-way protocol-70015 handshake without `PeerAllowed()` or an authorized-peer list. Both nodes remained at height 0 and no blocks were mined.

Evidence file:

```text
amlcore-peer-handshake-20260913_205259.txt
```

SHA-256:

```text
174b2764550ba6b9c9b8d8239aa8b5774b9a42f24cdd295b92ca3486d3ece3ab
```

## Forensic evidence hashes

The following local evidence reports were generated read-only from the preserved original binary:

```text
amltoken-fixed-seeds-raw.txt
SHA-256 b20be2cef4caf69981e05c28f6d7f9aeb61da1a3564fd35c2161d0516b71a065

amltoken-seedspec6-layout.txt
SHA-256 a03e08d242d3b2dcb7ad7fbc68fb0b18e0c0bca1acc800bdd7a08d401d04731d

amltoken-seed-mask-semantics.txt
SHA-256 a0ecfec5eb65231a7cd3706eb00ab423f83bdc654eb652cfc6decc0830dc03df
```

These hashes allow later comparison against the preserved working evidence without publishing holder-specific wallet material.

## What remains unresolved

Further forensic work is still required to determine the complete semantics of the custom `mask` field and every privilege associated with `PeerAllowed()` in the message-processing paths.

Those unresolved details do not change the evidence already established: the original AMLToken client contained a separate authorized-peer list and consulted it as an active peer-access control in the outbound connection path.

---

**Same genesis. Same historical ledger. Same ownership. No hidden peer gate in the revival.**
