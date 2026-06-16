# Store Data on Cell Terminal Proof

This proof was captured from a fresh terminal run of `node campaign-proof.js` against local OffCKB devnet RPC `http://localhost:28114`.

## Terminal Output

```text
$ node campaign-proof.js
Store Data on Cell campaign proof
devnet RPC: http://localhost:28114
created at: 2026-06-16T20:38:14.403Z

=== store-data-on-cell ===
[1] Encode and decode message
message: CKB cell proof: data lives in outputData on local devnet.
encoded hex: 0x434b422063656c6c2070726f6f663a2064617461206c6976657320696e206f757470757444617461206f6e206c6f63616c206465766e65742e
decoded text: CKB cell proof: data lives in outputData on local devnet.

[2] Building the transaction
sender address: ckt1qzda0cr08m85hc8jlnfp3zer7xulejywt49kt2rr0vthywaa50xwsqvarm0tahu0qfkq6ktuf3wd8azaas0h24c9myfz6
balance before: 4199893799995303 shannons
output[0].data: 0x434b422063656c6c2070726f6f663a2064617461206c6976657320696e206f757470757444617461206f6e206c6f63616c206465766e65742e
outputs count: 2
tx hash: 0xe2ab55ed411cfd54dc0c49fe0386eb2af2ab40528ffe24f6439974328eebf267

[3] Retrieving Live Cell data
out point: 0xe2ab55ed411cfd54dc0c49fe0386eb2af2ab40528ffe24f6439974328eebf267:0x0
live cell data: 0x434b422063656c6c2070726f6f663a2064617461206c6976657320696e206f757470757444617461206f6e206c6f63616c206465766e65742e
decoded live cell message: CKB cell proof: data lives in outputData on local devnet.
```

## Proof Details

| Detail | Value |
|--------|-------|
| **Message** | `CKB cell proof: data lives in outputData on local devnet.` |
| **Encoded hex** | `0x434b422063656c6c2070726f6f663a2064617461206c6976657320696e206f757470757444617461206f6e206c6f63616c206465766e65742e` |
| **Sender address** | `ckt1qzda0cr08m85hc8jlnfp3zer7xulejywt49kt2rr0vthywaa50xwsqvarm0tahu0qfkq6ktuf3wd8azaas0h24c9myfz6` |
| **Transaction hash** | `0xe2ab55ed411cfd54dc0c49fe0386eb2af2ab40528ffe24f6439974328eebf267` |
| **Out point** | `0xe2ab55ed411cfd54dc0c49fe0386eb2af2ab40528ffe24f6439974328eebf267:0x0` |
| **Decoded live cell message** | `CKB cell proof: data lives in outputData on local devnet.` |
