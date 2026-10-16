---
type: Secure Coding Rule
title: Use Copies When Modifying Iterables
description: Iterate over a copy of a list/dict/set when planning to modify the original inside the loop.
tags: [iteration, mutation, data-loss]
---

# Risk

Modifying a list/dict/set during iteration causes skipped elements or
`RuntimeError`. Silent data loss when items are missed.

# Mitigation

Iterate over `.copy()` or build a new collection; modify the original
separately.

# Non-compliant

```python
users = ['Alice', 'Bob', 'Bill', 'Charlie']
for user in users:
    if user.startswith('B'):
        users.remove(user)
# Result: ['Alice', 'Bill', 'Charlie'] — 'Bill' skipped
```

# Compliant

```python
users = ['Alice', 'Bob', 'Bill', 'Charlie']
for user in users.copy():
    if user.startswith('B'):
        users.remove(user)
# Result: ['Alice', 'Charlie']
```

# Examples

See [examples/pyscg-0031/](examples/pyscg-0031/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 8](https://github.com/ossf/secure-coding-guide-for-python)
