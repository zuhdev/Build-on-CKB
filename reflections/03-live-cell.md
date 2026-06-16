# Reflection: Retrieving Data from a Live Cell

**Step:** [3] Retrieving Live Cell Data  
**Out point:** `0xe2ab55ed411cfd54dc0c49fe0386eb2af2ab40528ffe24f6439974328eebf267:0x0`

After sending the transaction, I needed to verify the data actually made it on-chain. This involved retrieving the live Cell by its OutPoint — a combination of the transaction hash and output index.

The OutPoint `(txHash : 0x0)` uniquely identifies my message Cell anywhere on the chain. It's similar to how Bitcoin references UTXOs, but in CKB the focus is on the Cell as a stateful entity containing both capacity and data.

A challenge I encountered: Cells aren't available immediately after sending a transaction. They need to be mined first. The proof script implements a polling loop that retries every second for up to 20 seconds:

```javascript
async function waitForLiveCell(txHash, index = "0x0") {
  for (let attempt = 1; attempt <= 20; attempt++) {
    const cell = await client.getCellLive({ txHash, index }, true);
    if (cell) return cell;
    await sleep(1000);
  }
  throw new Error(`Live cell not found for ${txHash}:${index}`);
}
```

On the devnet, the cell was usually available within 1-2 seconds, but I could see how on testnet or mainnet this could take longer depending on network congestion.

The satisfying moment: decoding the retrieved `outputData` and seeing my original message come back. The hex (`0x434b42...`) decoded to "CKB cell proof: data lives in outputData on local devnet." — exactly what I put in.

This confirmed the full write/read cycle:
encode → build tx → send → mine → fetch by OutPoint → decode → original message

Each step is explicit, verifiable, and gives you full control over the data lifecycle on CKB.
