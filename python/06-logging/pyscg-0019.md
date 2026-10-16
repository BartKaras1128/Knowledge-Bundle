---
type: Secure Coding Rule
title: Exclude Sensitive Data From Logs
description: Never pass passwords, PII, or other sensitive variables to logging calls.
tags: [sensitive-logging, pii, gdpr, credentials]
---

# Risk

Logging passwords, credit cards, or PII violates GDPR/CCPA and exposes
credentials if logs are compromised (CWE-532, CWE-359).

# Mitigation

Never pass sensitive variables to logging calls; log only non-sensitive
identifiers like usernames or request IDs.

# Non-compliant

```python
import logging

def login_user(username, password, security_question):
    logging.info(
        "User %s login attempt: password=%s, security answer=%s",
        username, password, security_question
    )
```

# Compliant

```python
import logging

def login_user(username, password, security_question):
    logging.info("User %s login attempt", username)
    # password and security_question never reach the logger
```

# Examples

See [examples/pyscg-0019/](examples/pyscg-0019/).

# Related

See also [pyscg-0041 — Externalize Configuration and Secrets](../01-intro/pyscg-0041.md),
whose non-compliant example logs the same kind of secret this rule forbids.

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 6](https://github.com/ossf/secure-coding-guide-for-python)
