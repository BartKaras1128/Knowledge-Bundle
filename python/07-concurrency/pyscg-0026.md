---
type: Secure Coding Rule
title: Prevent Deadlocks
description: Never submit interdependent subtasks to the same bounded ThreadPoolExecutor; call the subtask inline instead.
tags: [concurrency, deadlock, thread-pool]
---

# Risk

Submitting nested tasks to the same bounded pool causes thread-starvation
deadlock when all workers block waiting on queued subtasks.

# Mitigation

Never submit interdependent subtasks to the same `ThreadPoolExecutor`; call
subtask logic inline or use a separate pool.

# Non-compliant

```python
from concurrent.futures import ThreadPoolExecutor

class Generator:
    def __init__(self):
        self.executor = ThreadPoolExecutor()

    def create_row(self, row):
        future = self.executor.submit(self.reformat, row)
        return future.result()  # Deadlock if pool saturated

    def reformat(self, row):
        return row.capitalize()
```

# Compliant

```python
from concurrent.futures import ThreadPoolExecutor

class Generator:
    def __init__(self):
        self.executor = ThreadPoolExecutor()

    def create_row(self, row):
        return self.reformat(row)  # Call inline, no nested submit

    def reformat(self, row):
        return row.capitalize()
```

# Examples

See [examples/pyscg-0026/](examples/pyscg-0026/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 7](https://github.com/ossf/secure-coding-guide-for-python)
