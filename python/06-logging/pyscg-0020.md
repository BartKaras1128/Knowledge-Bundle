---
type: Secure Coding Rule
title: Implement Informative Event Logging
description: Log all authentication attempts and authorization failures for audit trail purposes.
tags: [audit-logging, authentication, monitoring]
---

# Risk

Without audit logging of security events (auth failures, access denials),
brute-force attacks and breaches go undetected (CWE-778).

# Mitigation

Log all authentication attempts and authorization failures using the
`logging` module with structured messages forwarded to a central service.

# Non-compliant

```python
def login(username: str, password: str) -> bool:
    if username == "admin" and password == "s3cr3t":
        return True
    return False  # silent failure, no audit trail
```

# Compliant

```python
import logging
_audit = logging.getLogger("audit")

def login(username: str, password: str) -> bool:
    if username == "admin" and password == "s3cr3t":
        _audit.info("login_success user=%s", username)
        return True
    _audit.warning("login_failed user=%s", username)
    return False
```

# Examples

See [examples/pyscg-0020/](examples/pyscg-0020/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 6](https://github.com/ossf/secure-coding-guide-for-python)
