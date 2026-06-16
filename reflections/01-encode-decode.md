# Reflection: Encoding & Decoding Data on CKB

**Step:** [1] Encode and Decode Message

When I started this tutorial, I assumed storing data on a blockchain would involve some high-level API call. What I actually found was much more fundamental — CKB Cells store raw bytes, nothing else. If you want to put "hello world" on chain, you first turn it into hex.

The implementation in `campaign-proof.js` uses a pair of helper functions:

```javascript
function utf8ToHex(str) {
  const bytes = new TextEncoder().encode(str);
  return "0x" + Array.from(bytes).map(b => b.toString(16).padStart(2, "0")).join("");
}
```

I used `TextEncoder` and `TextDecoder` which are built into Node.js — no library needed. The pattern is straightforward:
- **Encode**: string → UTF-8 bytes → hex pairs → `0x`-prefixed string
- **Decode**: strip `0x` → parse hex pairs → bytes → UTF-8 string

A detail I found interesting: the `TextEncoder` always produces UTF-8 bytes, but `TextDecoder` is configurable. For CKB, UTF-8 is the standard, so `TextDecoder("utf-8")` works perfectly.

One thing I had to be careful about: the hex string must have an even number of characters (each byte is two hex chars). If you accidentally pass an odd-length string to `hexToUtf8()`, the `.match()` call drops the last character silently. Not a bug I hit, but worth keeping in mind.

The round-trip test was simple but essential — encode your message, decode it immediately, and confirm it matches. If it doesn't survive a round-trip in JavaScript, it definitely won't survive on-chain.
