# Reflection: Building a Transaction with Cell Data

**Step:** [2] Building the Transaction  
**Transaction hash:** `0xe2ab55ed411cfd54dc0c49fe0386eb2af2ab40528ffe24f6439974328eebf267`

This was the step where things felt real. After encoding the message, I had to actually package it into a transaction and send it to the chain.

The critical insight is that the data goes into `outputsData`, not as a separate message or event. In CKB, every Cell output can carry arbitrary bytes in its `data` field. My transaction had two outputs:
1. The message cell (with the encoded hex data)
2. The change cell (returning leftover capacity)

What tripped me up at first was the capacity requirement. Every byte of data in a Cell requires CKB tokens to be locked as capacity. The more data you store, the more CKB you need. For my 59-byte message, the cost was minimal, but it's a fundamentally different model from storing data in a database.

I used the `@ckb-ccc/core` SDK which handles a lot of the complexity:

```javascript
const tx = ccc.Transaction.from({
  outputs: [{ lock: address.script }],
  outputsData: [encoded],
});
await tx.completeInputsByCapacity(signer);
await tx.completeFeeBy(signer, 1000);
const txHash = await signer.sendTransaction(tx);
```

The `completeInputsByCapacity()` step was interesting — it automatically finds and uses your available Cells as inputs, calculates the total capacity, and sets up the change output. I didn't have to manually manage UTXOs like in Bitcoin.

One debugging moment: I initially forgot to add a fee output, and the transaction failed. The SDK's `completeFeeBy()` method handles this, but the fee of 1000 shannons (0.00001 CKB) is tiny compared to the locked capacity. It's worth understanding that fees and capacity are separate concerns in CKB.
