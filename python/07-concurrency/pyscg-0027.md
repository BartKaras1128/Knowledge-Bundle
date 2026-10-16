---
type: Secure Coding Rule
title: Prevent Race Conditions
description: Use threading.Lock around every compound read-modify-write sequence on shared state.
tags: [concurrency, race-condition, thread-safety, locking]
---

# Risk

Multiple threads modifying shared state without synchronization causes data
corruption; the GIL does not protect compound operations involving method
calls.

# Mitigation

Use `threading.Lock` around all compound read-modify-write sequences on
shared data.

# Non-compliant

```python
from threading import Thread

class Counter:
    value = 0
    def add(self):
        for _ in range(1000000):
            self.value += self.read_amount()
    def read_amount(self):
        return 100

c = Counter()
Thread(target=c.add).start()
Thread(target=c.add).start()  # Race condition
```

# Compliant

```python
import threading
from threading import Thread

class Counter:
    value = 0
    def __init__(self):
        self.lock = threading.Lock()
    def add(self):
        for _ in range(1000000):
            with self.lock:
                self.value += self.read_amount()
    def read_amount(self):
        return 100
```

# Examples

See [examples/pyscg-0027/](examples/pyscg-0027/).

# Related

See also [pyscg-0052 — Ensure Cleanup on Exceptions](../05-exception-handling/pyscg-0052.md)
for the safe way to acquire/release the lock used here.

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 7](https://github.com/ossf/secure-coding-guide-for-python)
