---
type: Secure Coding Rule
title: Implement Comparisons by Value Rather Than Reference
description: Define __eq__ (and __hash__ if needed) on classes used in comparisons or collections; without it, comparison is by identity.
tags: [equality, identity, comparison]
---

# Risk

Without `__eq__`, custom objects compare by identity. `==` and `in` silently
return `False` even for equal values, causing missed lookups and broken
collections.

# Mitigation

Implement `__eq__` (and `__hash__` if needed) on classes used in
comparisons or collections.

# Non-compliant

```python
class Integer:
    def __init__(self, value):
        self.value = value

print(Integer(12) == Integer(12))  # False
print(Integer(12) in [Integer(12)])  # False
```

# Compliant

```python
class Integer:
    def __init__(self, value):
        self.value = value
    def __eq__(self, other):
        if isinstance(other, type(self)):
            return self.value == other.value
        return NotImplemented
```

# Examples

See [examples/pyscg-0033/](examples/pyscg-0033/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 8](https://github.com/ossf/secure-coding-guide-for-python)
