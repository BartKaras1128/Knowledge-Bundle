---
type: Secure Coding Rule
title: Check for None Values
description: Guard with `if x is None` before accessing a potentially-None object; raise proper exceptions instead of raising None.
tags: [none, null-check, attributeerror]
---

# Risk

Calling methods on `None` raises `AttributeError`/`TypeError` at runtime,
causing crashes. Raising `None` instead of an exception produces an
unhelpful `TypeError`.

# Mitigation

Guard with `if x is None` before access; use `Optional` type hints; raise
proper exceptions.

# Non-compliant

```python
def is_valid_name(s: str) -> bool:
    names = s.split()  # crashes if s is None
    if len(names) != 2:
        return False
    return s.istitle()
```

# Compliant

```python
from typing import Optional

def is_valid_name(s: Optional[str]) -> bool:
    if s is None:
        return False
    names = s.split()
    if len(names) != 2:
        return False
    return s.istitle()
```

# Examples

See [examples/pyscg-0034/](examples/pyscg-0034/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 8](https://github.com/ossf/secure-coding-guide-for-python)
