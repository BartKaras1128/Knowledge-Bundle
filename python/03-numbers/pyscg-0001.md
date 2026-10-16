---
type: Secure Coding Rule
title: Control Numeric Precision
description: Use Decimal or integer cents for financial math instead of float.
tags: [precision, float, decimal, financial]
---

# Risk

Floating-point types have ~15-17 significant digits total. Financial
calculations using `float` silently produce incorrect results (e.g.
`3.00 - 5*0.33` -> `1.34999...`).

# Mitigation

Use integers (cents) or `decimal.Decimal` with string initialization for
precision-critical math.

# Non-compliant

```python
BALANCE = 3.00
ITEM_COST = 0.33
ITEM_COUNT = 5
result = BALANCE - ITEM_COUNT * ITEM_COST  # 1.349999...
```

# Compliant

```python
from decimal import Decimal
BALANCE = Decimal("3.00")
ITEM_COST = Decimal("0.33")
ITEM_COUNT = 5
result = BALANCE - ITEM_COUNT * ITEM_COST  # 1.35
```

# Examples

See [examples/pyscg-0001/](examples/pyscg-0001/).

# Related

See also [pyscg-0007 — Use String Literals for Decimal Construction](pyscg-0007.md)
and [pyscg-0005 — Specify Rounding for Numeric Conversions](pyscg-0005.md).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 3](https://github.com/ossf/secure-coding-guide-for-python)
