---
type: Secure Coding Rule
title: Check Return Values
description: Always assign the return value of immutable-object methods and check for sentinel values like -1 before using as index.
tags: [return-values, immutability, indexing]
---

# Risk

Ignoring return values of immutable-object methods (e.g. `str.replace()`)
means modifications are silently lost. Using `str.find()` result without
checking `-1` causes incorrect indexing.

# Mitigation

Always assign the return value; check for sentinel values like `-1` before
using as an index.

# Non-compliant

```python
def silly_string(user_input):
    user_input.replace("un", "very ")  # return value discarded
    return user_input  # original unchanged
```

# Compliant

```python
def silly_string(user_input):
    return user_input.replace("un", "very ")
```

# Examples

See [examples/pyscg-0036/](examples/pyscg-0036/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 8](https://github.com/ossf/secure-coding-guide-for-python)
