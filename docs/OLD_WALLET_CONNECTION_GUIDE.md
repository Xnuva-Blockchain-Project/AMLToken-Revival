# Old AMLToken / ABTC Wallet — Simple Connection Guide

> For historical AMLToken holders who still have an old wallet or computer.

## Q: I still have an old AMLToken / ABTC wallet. Can I connect it to the recovery nodes?

**Yes.** If your old AMLToken installation still works, it may be able to connect to the two public recovery nodes.

Before changing anything, **close AMLToken-Qt completely and make a backup of the entire AMLToken data folder**. Keep the original backup untouched.

The recovery nodes currently serve authenticated historical AMLToken blockchain data through block **175168**. If your old installation contains genuine later blockchain data, it may help recover more of the original AMLToken history.

## Q: I found an ABTC token or contract online. Is that the same thing?

**Not necessarily.** The ticker **ABTC** has been used by unrelated projects.

The recovery project described here concerns the **original native AMLToken/ABTC blockchain**, not an ERC-20 or BEP-20 token identified by a modern contract address.

Do not import an unrelated ABTC contract into a wallet or use it to judge the balance of your old AMLToken wallet.

For the legal history, ticker confusion and technical identity of the recovered chain, see:

**[AML Bitcoin, AMLToken and ABTC — Identity and Historical Context](ABTC_IDENTITY_AND_CONTEXT.md)**

## Q: Where is my AMLToken data folder?

The normal locations are:

| Operating system | Normal AMLToken data folder |
| --- | --- |
| Windows | `%APPDATA%\AMLToken` |
| Linux | `~/.amltoken` |
| macOS | `~/Library/Application Support/AMLToken` |

If the folder is not in the expected location, **do not create a new wallet or delete anything**. Your installation may have been configured to use a different location.

### Windows

1. Close AMLToken-Qt.
2. Press **Windows key + R**.
3. Enter:

```text
%APPDATA%\AMLToken
```

4. Press **Enter**.

If that does not open an AMLToken folder, enter `%APPDATA%` instead and look for a folder named **AMLToken**.

### Linux

1. Close AMLToken-Qt.
2. Open your Home folder.
3. The historical AMLToken folder is normally:

```text
.amltoken
```

Folders beginning with a dot are hidden. In many Linux file managers, press **Ctrl + H** to show hidden files.

### macOS

1. Close AMLToken-Qt.
2. In Finder choose **Go → Go to Folder**.
3. Enter:

```text
~/Library/Application Support/AMLToken
```

4. Press **Return**.

If you cannot find the folder, stop there and preserve the computer or drive as it is rather than reinstalling the wallet.

## Q: What should I back up?

Copy the **entire AMLToken data folder** to another safe location before editing anything.

Do not work on your only copy.

The folder may contain both your private wallet and historical blockchain files. The backup is for **you to keep privately**; do not upload the complete folder publicly.

## Q: How do I tell my wallet about the recovery nodes?

Inside the AMLToken data folder, look for:

```text
amltoken.conf
```

If it already exists, open it with a plain-text editor.

If it does not exist, create a plain-text file named exactly:

```text
amltoken.conf
```

Add these two lines:

```text
addnode=81.130.208.151:23247
addnode=84.247.164.62:23247
```

Save the file and restart AMLToken-Qt.

The wallet should then attempt to connect to the public AMLToken recovery nodes.

## Q: What if the wallet does not connect?

**Do not uninstall it, delete the data folder, create a new wallet, or overwrite the old files.**

Some surviving historical AMLToken clients may not connect cleanly because the original software contained historical peer-control behaviour. Even if the wallet cannot connect, its old blockchain files may still be extremely valuable to the recovery effort.

Preserve the original data folder and work only from a copy.

You can describe what you have in [GitHub Issue #2](https://github.com/Xnuva-Blockchain-Project/AMLToken-Revival/issues/2) without posting private wallet material.

## Q: What must I never send or publish?

**Never post or send:**

- `wallet.dat`;
- private keys;
- seed phrases;
- wallet passwords or passphrases;
- `dumpwallet` output;
- `dumpprivkey` output;
- your complete AMLToken data folder if it contains wallet material.

The recovery project needs **historical blockchain data**, not access to anybody's coins.

Useful non-private material may include `blocks/`, `blk*.dat`, later block height/hash information, public transaction IDs, old public installers, archived source code, or historical node information.

If you are unsure what is safe to share, describe the files you have **without uploading them first**.

## Q: What are the recovery nodes?

```text
Primary (T620):        81.130.208.151:23247
Secondary (Contabo):  84.247.164.62:23247
```

Both are walletless and non-mining archival/discovery nodes. They currently serve the independently validated historical AMLToken snapshot through height **175168**.

Height 175168 is the latest authenticated snapshot currently recovered. It is **not being claimed as the final historical AMLToken network tip**.

Any later blocks recovered from an old holder must still be preserved and independently validated before they are accepted as authentic historical continuation.

For a fuller explanation of what AMLToken Revival is recovering — and what unrelated modern ABTC tokens are not part of this chain — see [`ABTC_IDENTITY_AND_CONTEXT.md`](ABTC_IDENTITY_AND_CONTEXT.md).

---

**Keep the original safe. Work from a copy. Never share private keys or wallet files.**
