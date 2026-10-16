---
type: Secure Coding Rule
title: Validate Numeric Data Beyond Type Checking
description: Use math.isnan()/math.isfinite() to detect NaN and infinity; equality checks against NaN always return False.
tags: [nan, infinity, validation, float]
---

# Risk

`NaN` and `infinity` bypass numeric comparisons (NaN != NaN per IEEE 754),
corrupting calculations, statistics, and business logic silently (CWE-754).

# Mitigation

Use `math.isfinite()` or `math.isnan()` to validate float inputs before
arithmetic.

# Non-compliant

```python
def balance_is_positive(value: str) -> bool:
    _value = float(value)
    if _value == float("NaN"):  # always False
        raise ValueError("Expected a float")
    return _value > 0
```

# Compliant

```python
import math

def balance_is_positive(value: str) -> bool:
    _value = float(value)
    if math.isnan(_value):
        raise ValueError("Expected a float")
    return _value > 0
```

# Examples

See [examples/pyscg-0018/](examples/pyscg-0018/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 5](https://github.com/ossf/secure-coding-guide-for-python)
