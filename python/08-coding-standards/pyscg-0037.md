---
type: Secure Coding Rule
title: Presume Assertions May Be Disabled In Production
description: Use if/raise for any check required for correctness or security; assert statements are stripped by python -O.
tags: [assert, validation, production-safety]
---

# Risk

`python -O` strips all `assert` statements. Security/validation checks using
`assert` vanish in production, allowing invalid or malicious input through.

# Mitigation

Use `if ... raise ValueError/TypeError` for any check required for
correctness or security. Reserve `assert` for debug-only invariants.

# Non-compliant

```python
def my_exp(x):
    assert x in range(1, 710), f"Argument {x} is not valid"
    return math.exp(x)
# Bypassed with python -O
```

# Compliant

```python
def my_exp(x):
    if x not in range(1, 710):
        raise ValueError(f"Argument {x} is not valid")
    return math.exp(x)
```

# Examples

See [examples/pyscg-0037/](examples/pyscg-0037/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 8](https://github.com/ossf/secure-coding-guide-for-python)
