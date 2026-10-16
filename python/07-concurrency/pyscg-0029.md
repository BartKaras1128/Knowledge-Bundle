---
type: Secure Coding Rule
title: Reinitialize Reused Thread Objects
description: Reset thread-local state at the start or in a finally block of each task since pool workers are reused across tasks.
tags: [concurrency, thread-local, privilege-escalation, stale-state]
---

# Risk

Thread-local state persists across task executions on reused pool workers;
`initializer` only runs once per worker creation, not per task, leading to
privilege escalation or stale data.

# Mitigation

Reset thread-local state in a `finally` block after each task or
reinitialize at the start of each task function.

# Non-compliant

```python
from concurrent.futures import ThreadPoolExecutor
from threading import local

session = local()

def work_as_admin():
    session.role = "ADMIN"
    do_work()
    # role persists for next task on same worker

def work_as_guest():
    do_work()  # May inherit ADMIN from previous task
```

# Compliant

```python
def work_as_admin():
    try:
        session.role = "ADMIN"
        do_work()
    finally:
        session.role = "GUEST"  # Always reset

def work_as_guest():
    session.role = "GUEST"  # Explicit reinit
    do_work()
```

# Examples

See [examples/pyscg-0029/](examples/pyscg-0029/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 7](https://github.com/ossf/secure-coding-guide-for-python)
