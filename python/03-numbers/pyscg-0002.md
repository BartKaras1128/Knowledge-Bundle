---
type: Secure Coding Rule
title: Guard Fixed-Width Numbers Against Overflow
description: Validate inputs against type bounds before operating on fixed-width numeric types.
tags: [overflow, numpy, fixed-width]
---

# Risk

Fixed-width types (numpy, `datetime.timedelta`, `math.exp`) use C internally
and overflow silently or crash with `OverflowError` on boundary values.

# Mitigation

Validate inputs against type bounds and catch `OverflowError`/`RuntimeWarning`
before operating on fixed-width numbers.

# Non-compliant

```python
import numpy
a = numpy.int64(numpy.iinfo(numpy.int64).max)
print(a + 1)  # wraps to -9223372036854775808
```

# Compliant

```python
import warnings, numpy
warnings.filterwarnings("error")
a = numpy.int64(numpy.iinfo(numpy.int64).max)
try:
    print(a + 1)
except Warning:
    print("Overflow detected")
```

# Examples

See [examples/pyscg-0002/](examples/pyscg-0002/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 3](https://github.com/ossf/secure-coding-guide-for-python)
