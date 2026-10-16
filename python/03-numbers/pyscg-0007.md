---
type: Secure Coding Rule
title: Use String Literals for Decimal Construction
description: Always construct Decimal from a string literal, never from a float.
tags: [decimal, float, precision]
---

# Risk

`Decimal(0.45)` preserves the float's binary approximation, producing
`0.4500000000000000111...` instead of exact `0.45`.

# Mitigation

Always pass string literals to the `Decimal` constructor.

# Non-compliant

```python
from decimal import Decimal
print(Decimal(0.45))  # 0.450000000000000011102230246251...
```

# Compliant

```python
from decimal import Decimal
print(Decimal("0.45"))  # 0.45
```

# Examples

See [examples/pyscg-0007/](examples/pyscg-0007/).

# Related

See also [pyscg-0001 — Control Numeric Precision](pyscg-0001.md).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 3](https://github.com/ossf/secure-coding-guide-for-python)
