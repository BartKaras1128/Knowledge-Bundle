---
type: Secure Coding Rule
title: Ensure Correct Operator Precedence
description: Avoid obfuscated bitwise/precedence tricks that hide logic errors and make code unmaintainable.
tags: [readability, operator-precedence, maintainability]
---

# Risk

Obfuscated bitwise/precedence tricks hide logic errors, making code
unmaintainable and prone to silent correctness bugs when extended (CWE-783).

# Mitigation

Use explicit conditional branches with at most one write per expression;
prefer readable if/else over bitmask encoding.

# Non-compliant

```python
def label(number: int) -> list[str]:
    key = int(number < 5)
    key |= ((number & 1) ^ 1) << 1
    key |= (number < 0) << 2
    key |= (number > 0) << 3
    permuted = tuple(parts[(i * 5) & 7] for i in range(8))
    idx = (key * 5) & 7
    return permuted[idx].split(" ")
```

# Compliant

```python
def label(number: int) -> list[str]:
    labels = []
    if number < 0:
        labels.append("neg")
    if number % 2 == 0:
        labels.append("even")
    if number < 5:
        labels.append("small")
    if number >= 5:
        labels.append("big")
    return labels
```

# Examples

See [examples/pyscg-0042/](examples/pyscg-0042/).

# Related

See also [pyscg-0003 — Use Arithmetic Over Bitwise Operations](../03-numbers/pyscg-0003.md)
for the numeric-correctness side of bitwise operator misuse.

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 1](https://github.com/ossf/secure-coding-guide-for-python)
