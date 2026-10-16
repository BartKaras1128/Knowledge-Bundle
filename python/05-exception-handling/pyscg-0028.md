---
type: Secure Coding Rule
title: Preserve Exceptions in Finally Blocks
description: Never use return, break, or continue inside a finally block; doing so silently discards the active exception.
tags: [exception-handling, finally, control-flow]
---

# Risk

A `return`, `break`, or `continue` in a `finally` block silently discards the
active exception, masking errors (CWE-584).

# Mitigation

Never use `return`/`break`/`continue` that exits a `finally` block; place
returns after the try-finally.

# Non-compliant

```python
def do_logic():
    try:
        raise Exception
    finally:
        print("logic done")
        return True  # exception silently discarded
```

# Compliant

```python
def do_logic():
    try:
        raise Exception
    finally:
        print("logic done")
    return True
```

# Examples

See [examples/pyscg-0028/](examples/pyscg-0028/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 5](https://github.com/ossf/secure-coding-guide-for-python)
