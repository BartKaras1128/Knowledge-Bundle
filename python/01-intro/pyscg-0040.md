---
type: Secure Coding Rule
title: Use Process Isolation for Trust Zones
description: Run components with different trust levels under separate OS users so breaching one does not grant access to all.
tags: [process-isolation, trust-boundary, defense-in-depth]
---

# Risk

Running all Python runtimes under the same POSIX user means breaching one
component grants full access to all others — no defense in depth (CWE-653).

# Mitigation

Run each trust zone under a separate POSIX/machine user with least-privilege
access rights; require authentication/authorization to cross zone boundaries.

# Non-compliant

```python
# All services (web, DB, admin) running as single user "appuser"
# Breaching the outer perimeter gives attacker full system access
# No authentication required between internal components
```

# Compliant

```python
# Each zone runs under a different user:
#   web_user  -> handles HTTP (restricted network access)
#   db_user   -> database operations only
#   admin_user -> management plane (MFA required)
# Crossing trust boundaries requires mTLS + RBAC
```

# Examples

See [examples/pyscg-0040/](examples/pyscg-0040/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 1](https://github.com/ossf/secure-coding-guide-for-python)
