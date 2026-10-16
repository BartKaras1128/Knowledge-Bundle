---
type: Secure Coding Rule
title: Handle Error Conditions
description: Wrap file I/O in try/except blocks catching specific OSError subclasses instead of letting exceptions crash silently.
tags: [exception-handling, file-io, error-handling]
---

# Risk

Unhandled file I/O exceptions crash the program silently or leave resources
in undefined states (CWE-755).

# Mitigation

Wrap I/O operations in `try/except` blocks catching specific `OSError`
subclasses, then log or recover.

# Non-compliant

```python
import os

def read_file(file):
    fd = os.open(file, os.O_RDONLY)
    content = os.read(fd, 1024)
    return content.decode()
```

# Compliant

```python
import os

def read_file(file):
    try:
        fd = os.open(file, os.O_RDONLY)
        try:
            content = os.read(fd, 1024)
        finally:
            os.close(fd)
        return content.decode()
    except OSError as e:
        print(f"An error occurred: {e}")
```

# Examples

See [examples/pyscg-0015/](examples/pyscg-0015/).

# Related

See also [pyscg-0052 — Ensure Cleanup on Exceptions](pyscg-0052.md) for the
resource-cleanup half of this pattern (using `with`/`finally`).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 5](https://github.com/ossf/secure-coding-guide-for-python)
