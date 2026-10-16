---
type: Secure Coding Rule
title: Use Arithmetic Over Bitwise Operations
description: Avoid bitwise shift operators for multiplication/division; their precedence and negative-number semantics differ from arithmetic operators.
tags: [bitwise, operator-precedence, arithmetic]
---

# Risk

Bitwise shifts mixed with arithmetic have unexpected precedence
(`8 << 2 + 10` -> 32768, not 42). Right-shifting negative numbers truncates
toward negative infinity, not zero.

# Mitigation

Replace bitwise shifts used for multiplication/division with `*` and `/`
operators.

# Non-compliant

```python
print(8 << 2 + 10)  # 32768, not 42
foo = -50
foo >>= 2  # -13, not -12
```

# Compliant

```python
print(8 * 4 + 10)  # 42
foo = -50
bar = foo / 4  # -12.5
```

# Examples

See [examples/pyscg-0003/](examples/pyscg-0003/).

# Related

See also [pyscg-0042 — Ensure Correct Operator Precedence](../01-intro/pyscg-0042.md)
for the broader readability/maintainability angle on bitwise operator misuse.

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 3](https://github.com/ossf/secure-coding-guide-for-python)
