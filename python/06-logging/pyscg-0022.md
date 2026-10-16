---
type: Secure Coding Rule
title: Neutralize Untrusted Data in Logs
description: Validate input against an allow-list before logging to prevent log injection and forged entries.
tags: [log-injection, crlf, allow-list]
---

# Risk

Unsanitized user input with CRLF sequences allows attackers to forge log
entries, hide malicious activity, or inject XSS into log viewers (CWE-117,
CWE-93).

# Mitigation

Validate input against a strict allow-list before logging; use `%r` for
rejected values to escape control characters.

# Non-compliant

```python
import logging

def log_authentication_failed(user):
    logging.warning("User login failed for: '%s'", user)

# Attacker injects: "guest'\nWARNING:root:User login failed for: 'admin"
```

# Compliant

```python
import logging
import re

_ALLOWED_USER = re.compile(r"^[A-Za-z0-9._-]{1,64}$")

def log_authentication_failed(user):
    if not _ALLOWED_USER.fullmatch(user):
        logging.warning("Rejected login: invalid username=%r", user)
        return
    logging.warning("User login failed for: '%s'", user)
```

# Examples

See [examples/pyscg-0022/](examples/pyscg-0022/).

# Related

See also [pyscg-0047 — Use Allow Lists Over Deny Lists](../04-neutralization/pyscg-0047.md).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 6](https://github.com/ossf/secure-coding-guide-for-python)
