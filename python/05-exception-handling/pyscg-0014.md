---
type: Secure Coding Rule
title: Use Specific Exception Types
description: Raise the most specific exception type that matches the error condition instead of a generic Exception.
tags: [exception-handling, error-handling]
---

# Risk

Raising generic `Exception` or `BaseException` prevents callers from
handling errors specifically, hiding bugs and breaking targeted recovery
logic.

# Mitigation

Raise the most specific built-in or custom exception that matches the error
condition.

# Non-compliant

```python
def divide(divided: int, divisor: int) -> float:
    if divisor == 0:
        raise Exception("Cannot divide by zero")
    return divided / divisor
```

# Compliant

```python
def divide(divided: int, divisor: int) -> float:
    if divisor == 0:
        raise ZeroDivisionError("Cannot divide by zero")
    return divided / divisor
```

# Examples

See [examples/pyscg-0014/](examples/pyscg-0014/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 5](https://github.com/ossf/secure-coding-guide-for-python)
