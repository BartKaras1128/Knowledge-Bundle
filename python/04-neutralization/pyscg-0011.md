---
type: Secure Coding Rule
title: Prevent Type Confusion
description: Explicitly cast external inputs at trust boundaries; type hints are not enforced at runtime.
tags: [type-confusion, validation, trust-boundary]
---

# Risk

Type hints aren't enforced at runtime; `100 * "3"` repeats the string
instead of multiplying.

# Mitigation

Explicitly cast external inputs at trust boundaries.

# Non-compliant

```python
def shopping_bag(price: int, qty: int) -> int:
    return price * qty  # "3" * 100 = "333...3"
```

# Compliant

```python
def shopping_bag(price: int, qty: int) -> int:
    return int(price) * int(qty)
```

# Examples

See [examples/pyscg-0011/](examples/pyscg-0011/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 4](https://github.com/ossf/secure-coding-guide-for-python)
