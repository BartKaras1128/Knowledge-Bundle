---
type: Secure Coding Rule
title: Ensure Cleanup on Exceptions
description: Use context managers (with statements) to guarantee resource cleanup regardless of exceptions.
tags: [resource-cleanup, context-manager, deadlock, exception-handling]
---

# Risk

Resources (locks, file handles, connections) remain acquired when exceptions
interrupt code before manual release, causing deadlocks or leaks (CWE-460).

# Mitigation

Use `with` statements (context managers) to guarantee cleanup regardless of
exceptions.

# Non-compliant

```python
import threading
lock = threading.Lock()

def perform_critical_operation():
    lock.acquire()
    print("Performing operation...")
    raise ValueError("Something went wrong!")
    lock.release()  # never reached
```

# Compliant

```python
import threading
lock = threading.Lock()

def perform_critical_operation():
    with lock:
        print("Performing operation...")
        raise ValueError("Something went wrong!")
    # lock released automatically
```

# Examples

See [examples/pyscg-0052/](examples/pyscg-0052/).

# Related

See also [pyscg-0051 — Release Unused Resources](../08-coding-standards/pyscg-0051.md)
and [pyscg-0027 — Prevent Race Conditions](../07-concurrency/pyscg-0027.md).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 5](https://github.com/ossf/secure-coding-guide-for-python)
