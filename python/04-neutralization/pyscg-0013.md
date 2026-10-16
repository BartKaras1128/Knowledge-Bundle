---
type: Secure Coding Rule
title: Secure Search Paths
description: Run Python in isolated mode with hash-based pyc verification to prevent module search-path injection.
tags: [pythonpath, module-injection, isolation]
---

# Risk

An attacker controlling `PYTHONPATH` injects malicious modules that get
loaded instead of legitimate ones.

# Mitigation

Run with `-I` (isolated) and `--check-hash-based-pycs always`.

# Non-compliant

```bash
python3 -m http.server -b 127.0.0.42 8080
```

# Compliant

```bash
python3 -I --check-hash-based-pycs always -m http.server -b 127.0.0.42 8080
```

# Examples

See [examples/pyscg-0013/](examples/pyscg-0013/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 4](https://github.com/ossf/secure-coding-guide-for-python)
