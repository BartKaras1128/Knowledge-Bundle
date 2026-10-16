---
type: Secure Coding Rule
title: Avoid Redefining Built-in Functions or Standard Library Identifiers
description: Never reuse names like len, str, or os for your own functions/classes; it silently breaks all downstream code.
tags: [shadowing, naming, maintainability]
---

# Risk

Shadowing `len`, `str`, `os`, etc. breaks all downstream code relying on the
original, causing crashes or incorrect results with no obvious traceback.

# Mitigation

Use unique names (e.g. `custom_len`); never reuse stdlib identifiers.

# Non-compliant

```python
def len(numbers: list[int]) -> int:
    result = 0
    for number in numbers:
        result += number
    return result
# Built-in len() is now broken for the entire module
```

# Compliant

```python
def sum_numbers(numbers: list[int]) -> int:
    result = 0
    for number in numbers:
        result += number
    return result
```

# Examples

See [examples/pyscg-0032/](examples/pyscg-0032/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 8](https://github.com/ossf/secure-coding-guide-for-python)
