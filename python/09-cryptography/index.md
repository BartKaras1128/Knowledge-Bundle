---
okf_version: "0.1"
---

# Chapter 9 — Cryptography

Secure use of random number generation in Python. The `random` module uses
the deterministic Mersenne Twister (MT19937) algorithm and is unsuitable for
security-sensitive contexts. Cryptographic randomness must come from
`secrets` or `os.urandom()`.

# Rules

* [pyscg-0038 — Use Sufficiently Random Values](pyscg-0038.md) - use secrets module for tokens/keys/session IDs
