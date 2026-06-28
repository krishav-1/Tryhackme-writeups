# TryHackMe — Wise Guy

**Platform:** [TryHackMe](https://tryhackme.com)  
**Difficulty:** Easy  
**Category:** Cryptography / Enumeration  
**Status:** ✅ Completed

---

## Overview

A challenge involving service enumeration and XOR cryptanalysis. The goal was to connect to a custom service, receive an encrypted message, and recover the flag using known-plaintext XOR analysis.

---

## Tools Used

| Tool | Purpose |
|------|---------|
| `netcat (nc)` | Connect to the target service |
| [CyberChef](https://gchq.github.io/CyberChef/) | XOR encryption/decryption and key recovery |

---

## Methodology

### Step 1 — Service Enumeration

Connected to the target on port `1337` using Netcat to see what was being served:

```bash
nc <target-ip> 1337
```

The service responded with an XOR-encrypted ciphertext.

---

### Step 2 — XOR Key Recovery (Known-Plaintext Attack)

The only hint provided was that the first flag began with `THM{`.

XOR has a useful property: if you know part of the plaintext, you can recover the key:

```
key = ciphertext XOR known_plaintext
```

Using **CyberChef**, I applied the following recipe:

1. **XOR** the ciphertext against the known plaintext `THM{` to extract the repeating key
2. **From XOR** to identify the full key pattern
3. **XOR** the full ciphertext using the recovered key to reveal the plaintext flag

This is a **known-plaintext attack** — a classic technique in XOR cryptanalysis.

---

### Step 3 — Flag Recovery

With the key recovered, decrypting the full ciphertext revealed the flag.

> **Flag:** `THM{REDACTED}`

---

## Key Takeaways

- XOR encryption is **not secure** when any portion of the plaintext is known — the key can be trivially recovered
- Repeating-key XOR (also known as Vigenère-style XOR) is especially vulnerable to known-plaintext attacks
- **CyberChef** is an excellent browser-based tool for rapid crypto analysis during CTFs
- Custom TCP services on unusual ports (like 1337) are always worth enumerating manually with Netcat

---

## References

- [CyberChef](https://gchq.github.io/CyberChef/) — GCHQ's web-based crypto/encoding toolkit
- [XOR cipher — Wikipedia](https://en.wikipedia.org/wiki/XOR_cipher)
- [TryHackMe](https://tryhackme.com)
