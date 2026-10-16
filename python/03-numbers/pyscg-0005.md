---
type: Secure Coding Rule
title: Specify Rounding for Numeric Conversions
description: Use Decimal.quantize with an explicit rounding mode instead of relying on int()/round() defaults.
tags: [rounding, decimal, financial]
---

# Risk

`int()` truncates toward zero and `round()` uses bankers' rounding
(round-half-to-even), which may silently produce wrong results in financial
or safety-critical code.

# Mitigation

Use `Decimal.quantize()` with an explicit rounding mode (e.g.
`ROUND_HALF_UP`).

# Non-compliant

```python
print(int(0.5))    # 0 (truncates)
print(round(0.5))  # 0 (bankers' rounding)
print(round(1.5))  # 2
```

# Compliant

```python
from decimal import Decimal, ROUND_HALF_UP
print(Decimal("0.5").quantize(Decimal("1"), rounding=ROUND_HALF_UP))  # 1
print(Decimal("1.5").quantize(Decimal("1"), rounding=ROUND_HALF_UP))  # 2
```

# Examples

See [examples/pyscg-0005/](examples/pyscg-0005/).

# Related

See also [pyscg-0001 — Control Numeric Precision](pyscg-0001.md).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 3](https://github.com/ossf/secure-coding-guide-for-python)
