---
type: Secure Coding Rule
title: Use an Appropriate Comparator for Numbers
description: Compare numeric types directly instead of comparing their stringified representations.
tags: [comparison, float, decimal]
---

# Risk

Comparing stringified floats fails because `str(4/2)` is `"2.0"`, not `"2"`.
Logic branches are silently skipped.

# Mitigation

Compare using numeric types (`Decimal.compare()`, `math.isclose()`, or
`fractions`) instead of string representations.

# Non-compliant

```python
s = str(4 / 2)
if s == "2":
    print("equal")  # never reached — s is "2.0"
```

# Compliant

```python
from decimal import Decimal
t = Decimal(str(4 / 2))
if Decimal("2").compare(t) == 0:
    print("equal")  # works
```

# Examples

See [examples/pyscg-0006/](examples/pyscg-0006/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 3](https://github.com/ossf/secure-coding-guide-for-python)
