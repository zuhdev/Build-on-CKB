# Build on CKB — Campaign 02: Store Data on Cell

**Quest:** Complete the OffCKB quick start and Store Data on Cell tutorial.  
**Submitted by:** [zuhdev](https://github.com/zuhdev)  
**Date:** 2026-06-16

---

## Environment

| Setting | Value |
|---|---|
| Tutorial | Store Data on Cell |
| Local chain | OffCKB devnet |
| RPC endpoint | `http://localhost:28114` |
| Script | `node src/campaign-proof.js` |
| Source | Official Nervos Store Data on Cell tutorial |

Raw terminal transcript: [`terminal-output.txt`](terminal-output.txt) · Full proof: [`proof-output.md`](proof-output.md)

---

## Proof Details

### 1. Encode and Decode Message

```text
Message:   CKB cell proof: data lives in outputData on local devnet.
Encoded:   0x434b422063656c6c2070726f6f663a2064617461206c6976657320…
Decoded:   CKB cell proof: data lives in outputData on local devnet.
```

The UTF-8 message was encoded into Cell-compatible hex via `utf8ToHex()` and decoded back to the original text via `hexToUtf8()`.

### 2. Building the Transaction

| Field | Value |
|---|---|
| Sender address | `ckt1qzda0cr08m85hc8jlnfp3zer7xulejywt49kt2rr0vthywaa50xwsqvarm0tahu0qfkq6ktuf3wd8azaas0h24c9myfz6` |
| Output data | `0x434b422063656c6c2070726f6f663a2064617461206c6976657320696e206f757470757444617461206f6e206c6f63616c206465766e65742e` |
| Outputs count | 2 |
| Transaction hash | `0xe2ab55ed411cfd54dc0c49fe0386eb2af2ab40528ffe24f6439974328eebf267` |

The transaction was assembled with the encoded message in `output[0].data`, signed, and sent on the local devnet.

### 3. Retrieving Live Cell Data

| Field | Value |
|---|---|
| Out point | `0xe2ab55ed411cfd54dc0c49fe0386eb2af2ab40528ffe24f6439974328eebf267:0x0` |
| Live cell data | `0x434b422063656c6c2070726f6f663a2064617461206c6976657320696e206f757470757444617461206f6e206c6f63616c206465766e65742e` |
| Decoded message | `CKB cell proof: data lives in outputData on local devnet.` |

The live Cell at output index 0 was retrieved by its OutPoint and the `outputData` was decoded back to the original message, confirming the write/read cycle.

---

## Reflections

Detailed reflections for each step of the process:

| Step | Reflection |
|---|---|
| 1. Encode & Decode | [`reflections/01-encode-decode.md`](reflections/01-encode-decode.md) |
| 2. Build Transaction | [`reflections/02-build-transaction.md`](reflections/02-build-transaction.md) |
| 3. Retrieve Live Cell | [`reflections/03-live-cell.md`](reflections/03-live-cell.md) |

---

## Files

```
├── README.md              # Submission document
├── proof-output.md        # Detailed proof output reference
├── terminal-output.txt    # Raw terminal transcript
├── .gitignore             # Git ignore rules
├── src/
│   ├── campaign-proof.js  # CLI proof script
│   ├── system-scripts.json# Devnet script configs
│   ├── package.json       # Dependencies
│   └── package-lock.json  # Lockfile
├── reflections/           # Step-by-step learnings
│   ├── 01-encode-decode.md
│   ├── 02-build-transaction.md
│   └── 03-live-cell.md
└── screenshots/           # Proof screenshots
    ├── 00-terminal-output.png
    ├── 01-encode-decode.png
    ├── 02-build-transaction.png
    └── 03-live-cell.png
```
