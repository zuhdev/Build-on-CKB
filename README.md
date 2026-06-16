# Build on CKB — Campaign 02: Store Data on Cell


---

## Environment

| Setting | Value |
|---|---|
| Tutorial | Store Data on Cell |
| Local chain | OffCKB devnet |
| RPC endpoint | `http://localhost:28114` |
| Script | `node src/campaign-proof.js` |

---

## Proof of Completion

### ✅ Step 1: Encode & Decode Message

| | |
|---|---|
| **Original message** | `CKB cell proof: data lives in outputData on local devnet.` |
| **Encoded hex** | `0x434b422063656c6c2070726f6f663a2064617461206c6976657320…` |
| **Decoded result** | `CKB cell proof: data lives in outputData on local devnet.` |

The UTF-8 message was encoded into Cell-compatible hex via `utf8ToHex()` and decoded back to original text via `hexToUtf8()`, confirming a clean round-trip.

### ✅ Step 2: Build & Send Transaction

| | |
|---|---|
| **Sender address** | `ckt1qzda0cr08m85hc8jlnfp3zer7xulejywt49kt2rr0vthywaa50xwsqvarm0tahu0qfkq6ktuf3wd8azaas0h24c9myfz6` |
| **Output data** | `0x434b422063656c6c2070726f6f663a2064617461206c6976657320696e206f757470757444617461206f6e206c6f63616c206465766e65742e` |
| **Outputs** | 2 (message cell + change cell) |
| **Transaction hash** | `0xe2ab55ed411cfd54dc0c49fe0386eb2af2ab40528ffe24f6439974328eebf267` |

### ✅ Step 3: Retrieve Live Cell Data

| | |
|---|---|
| **Out point** | `0xe2ab55ed411cfd54dc0c49fe0386eb2af2ab40528ffe24f6439974328eebf267:0x0` |
| **Live cell data** | `0x434b422063656c6c2070726f6f663a2064617461206c6976657320696e206f757470757444617461206f6e206c6f63616c206465766e65742e` |
| **Decoded message** | `CKB cell proof: data lives in outputData on local devnet.` |

The live Cell at output index 0 was retrieved by its OutPoint and decoded — confirming the write/read cycle.

---

## Reflections

| Step | Reflection |
|---|---|
| 1. Encode & Decode | [`reflections/01-encode-decode.md`](reflections/01-encode-decode.md) |
| 2. Build Transaction | [`reflections/02-build-transaction.md`](reflections/02-build-transaction.md) |
| 3. Retrieve Live Cell | [`reflections/03-live-cell.md`](reflections/03-live-cell.md) |

---

## Supporting Files

- [`terminal-output.txt`](terminal-output.txt) — Raw terminal transcript
- [`proof-output.md`](proof-output.md) — Detailed proof output
- [`src/campaign-proof.js`](src/campaign-proof.js) — CLI proof script
