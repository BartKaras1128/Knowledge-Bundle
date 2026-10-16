---
type: Secure Coding Rule
title: Use Sufficiently Random Values
description: Use the secrets module, not random, for any security-sensitive random value generation.
tags: [weak-randomness, cryptography, tokens, secrets]
---

# Risk

Python's `random` module is deterministic (Mersenne Twister). An attacker
who knows or guesses the seed can predict all generated values,
compromising tokens, keys, and session identifiers.

# Mitigation

Use the `secrets` module for any security-sensitive random value
generation.

# Non-compliant

```python
import random

def generate_web_token():
    """Predictable — Mersenne Twister is deterministic"""
    return random.randrange(int("1" + "0" * 31), int("9" * 32), 1)

TOKEN = generate_web_token()
```

# Compliant

```python
import secrets

def generate_web_token():
    """Cryptographically secure via os.urandom()"""
    return secrets.token_urlsafe()

TOKEN = generate_web_token()
```

# Examples

See [examples/pyscg-0038/](examples/pyscg-0038/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 9](https://github.com/ossf/secure-coding-guide-for-python)
