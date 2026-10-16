---
type: Secure Coding Rule
title: Use Integer Loop Counters
description: Use integer loop counters instead of float counters to avoid rounding-error accumulation.
tags: [float, loop, rounding]
---

# Risk

Float loop counters accumulate rounding errors, causing missed conditions
(`0.1+0.1+...` never equals `0.8`) or infinite loops when the increment is
below float precision.

# Mitigation

Use `int` counters and convert to float only when needed for computation.

# Non-compliant

```python
counter = 0.0
while counter <= 1.0:
    if counter == 0.8:
        break  # never reached
    counter += 0.1
```

# Compliant

```python
counter = 0
while counter <= 10:
    if counter / 10 == 0.8:
        break
    counter += 1
```

# Examples

See [examples/pyscg-0004/](examples/pyscg-0004/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 3](https://github.com/ossf/secure-coding-guide-for-python)
