---
type: Secure Coding Rule
title: Canonicalize Input Before Validating
description: Normalize Unicode input with NFKC before running any pattern-based validation, never after.
tags: [unicode, normalization, validation-bypass, injection]
---

# Risk

Unicode characters like ONE DOT LEADER (`\u2024`) or FULLWIDTH SOLIDUS
(`\uff0f`) bypass ASCII-based validation checks, enabling directory
traversal and injection attacks when normalization happens after (or
without) validation.

# Mitigation

Normalize input with `unicodedata.normalize("NFKC", ...)` *before* any
validation or pattern matching.

# Non-compliant

```python
import re
import unicodedata

def validate(suspicious_string: str):
    if re.search("./", suspicious_string):
        raise ValueError("Attack detected")
    # Normalizing AFTER check — attacker uses \u2024\uff0f to bypass
    normalized = unicodedata.normalize("NFKC", suspicious_string)
    return normalized

validate("\u2024\u2024\uff0f" + "passwd")  # No exception raised
```

# Compliant

```python
import re
import unicodedata

def validate(suspicious_string: str):
    normalized = unicodedata.normalize("NFKC", suspicious_string)
    if re.search("./", normalized):
        raise ValueError("Attack detected")
    return normalized

validate("\u2024\u2024\uff0f" + "passwd")  # Raises ValueError
```

# Examples

See [examples/pyscg-0044/](examples/pyscg-0044/).

# Related

See also [pyscg-0009 — Prevent OS Command Injection](../04-neutralization/pyscg-0009.md)
and [pyscg-0012 — Extract Archives Safely](../04-neutralization/pyscg-0012.md), both of
which are downstream of path validation that this Unicode bypass can defeat.

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 2](https://github.com/ossf/secure-coding-guide-for-python)
