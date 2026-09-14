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

## All direct `PeerAllowed()` call sites

A complete static call-site sweep of the preserved binary found exactly **five direct calls** to `PeerAllowed()`.

DWARF line information resolves them to the following original AMLCore source locations:

| Binary call address | Original function | Recovered source location | Control category |
| --- | --- | --- | --- |
| `0x1dcb12` | `CConnman::OpenNetworkConnection(...)` | `src/net.cpp:1982` | outbound connection access control |
| `0x1e082a` | `CConnman::AttemptToEvictConnection()` | `src/net.cpp:963` | peer-eviction protection / privilege |
| `0x20d043` | `ProcessMessage(...)` | `src/net_processing.cpp:1461` | address-message handling |
| `0x2113c4` | `ProcessMessage(...)` | `src/net_processing.cpp:2393` | block-message handling |
| `0x212b5e` | `ProcessMessage(...)` | `src/net_processing.cpp:1956` | compact-block handling |

The exact upstream Bitcoin Core baseline has no `PeerAllowed()` call at these locations. In the baseline, the corresponding regions are normal connection, eviction, `ADDR`, `BLOCK`, and `CMPCTBLOCK` processing. The authorization mechanism is therefore an AMLToken-specific addition rather than inherited Bitcoin behaviour.

### 1. Outbound connection path

At `CConnman::OpenNetworkConnection(...)`, the result of `PeerAllowed()` is used as a branch condition before the connection continues through the normal outbound path.

This is the strongest access-control finding: the historical client did not simply use the authorized list as metadata. Membership affected whether an outbound peer could proceed normally.

### 2. Peer-eviction path

`CConnman::AttemptToEvictConnection()` also consults `PeerAllowed()`.

The observed branch behaviour protects an authorized peer from the normal eviction-candidate path. This grants the authorized set preferential connection-retention treatment in addition to the ordinary Bitcoin eviction protections.

This is one reason the revival must **not** implement decentralization by replacing `PeerAllowed()` with an unconditional `true`: doing so could accidentally grant every connected peer the historical privileged treatment.

### 3. Address-message path

A `PeerAllowed()` check occurs inside `ProcessMessage(...)` at the source region corresponding to Bitcoin's `ADDR` message processing.

The AMLToken branch changes handling of network-address information according to authorized status. This demonstrates that authorization reached beyond initial connection establishment into peer-discovery/message behaviour.

### 4. Block-message path

A `PeerAllowed()` check occurs in the `BLOCK` processing region.

Authorized status therefore influences the historical client's block-message processing path. The evidence establishes differentiated handling; it should not be described as a consensus exception. Nothing recovered so far shows that an authorized peer could make an otherwise consensus-invalid block valid.

### 5. Compact-block path

A fifth direct check occurs in the `CMPCTBLOCK` processing region.

Again, authorization affects P2P processing policy. It does not establish that authorized peers could bypass proof-of-work or block-validity consensus rules.

## What the five calls prove

Taken together, the five direct uses show that the historical authorization list was not a passive bootstrap list. It was consulted in multiple networking-policy layers:

- normal outbound connection progression;
- peer-retention/eviction policy;
- address propagation or intake handling;
- block-message handling;
- compact-block handling.

This is materially more centralized than ordinary Bitcoin-style fixed-seed discovery because the same operator-defined authorization concept affected both access and subsequent peer treatment.

The evidence currently establishes an **outbound peer authorization gate and additional authorized-peer networking privileges**. It should not be overstated as proof that every inbound TCP connection was rejected directly at `AcceptConnection()`; that specific claim has not been established.

It also should not be overstated as proof of a consensus backdoor. The recovered calls are networking and message-processing policy controls, not evidence that invalid blocks or transactions could bypass consensus validation.

## Why this mattered to holders

The historical software therefore depended on a small, explicitly defined authorized-peer set for normal outbound connectivity and granted that set additional networking treatment.

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

amltoken-peerallowed-all-call-sites-20260913_210817.txt
SHA-256 e09b05f97e6b480cc98de8ad22a74dc62fa8594718beeda9c4ab6356e2f9371a

amltoken-peerallowed-classification-20260914_120152.txt
SHA-256 08f0cf425471d118c7440b21f84ccd03e7e3411668e3a217538873ce6149e219
```

These hashes allow later comparison against the preserved working evidence without publishing holder-specific wallet material.

## Remaining network-control questions

The principal network-control architecture is now established: the authorized list, its 13 entries, its use by `PeerAllowed()`, the outbound gate, the eviction privilege, and the three message-processing call-site categories are all identified.

The custom `mask` field is passed into the `CService` constructor as a third 16-bit argument and is `128` in the recovered records. Its precise semantic purpose can be documented further if original source or additional symbol-level evidence is recovered, but that detail is not required to establish the authorization architecture.

Likewise, lower-level branch semantics inside the three message-processing call sites can be refined later without changing the central finding: authorized status altered peer handling beyond ordinary connection establishment.

---

**Same genesis. Same historical ledger. Same ownership. No hidden peer gate in the revival.**
