---
type: Secure Coding Rule
title: Propagate Exceptions and Preserve Context
description: Never use bare except; catch specific exception types so KeyboardInterrupt/SystemExit still propagate.
tags: [exception-handling, bare-except, denial-of-service]
---

# Risk

Bare `except:` catches `KeyboardInterrupt` and `SystemExit`, making programs
unkillable and hiding real errors (CWE-396).

# Mitigation

Catch specific exception types; re-raise with context using `from` when
wrapping.

# Non-compliant

```python
from time import sleep

def exception_example():
    while True:
        try:
            sleep(1)
            _ = 1 / 0
        except:
            print("Don't care")
```

# Compliant

```python
from time import sleep

def exception_example():
    while True:
        sleep(1)
        try:
            _ = 1 / 0
        except ZeroDivisionError:
            print("How is it now?")
```

# Examples

See [examples/pyscg-0016/](examples/pyscg-0016/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 5](https://github.com/ossf/secure-coding-guide-for-python)
