---
type: Secure Coding Rule
title: Secure Deserialization
description: Never pickle.loads() untrusted data; use JSON or HMAC-verify before unpickling.
tags: [injection, unsafe-deserialization, pickle, rce]
---

# Risk

`pickle.loads()` executes arbitrary code — attackers achieve RCE (real CVEs
at CVSS 9.8).

# Mitigation

Use JSON/YAML. If pickle is unavoidable, HMAC-verify before unpickling.

# Non-compliant

```python
import pickle
def uncan(self, jar):
    return pickle.loads(jar)  # RCE
```

# Compliant

```python
import json
def uncan(self, jar: str) -> Message:
    data = json.loads(jar)
    msg = Message()
    msg.sender_id = int(data["sender_id"])
    return msg
```

# Examples

See [examples/pyscg-0023/](examples/pyscg-0023/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 4](https://github.com/ossf/secure-coding-guide-for-python)
