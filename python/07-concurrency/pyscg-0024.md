---
type: Secure Coding Rule
title: Ensure Thread Pool Tasks Can Be Interrupted
description: Pass a threading.Event to each task and check it periodically instead of relying on future.cancel().
tags: [concurrency, thread-pool, denial-of-service, graceful-shutdown]
---

# Risk

Calling `future.cancel()` on an already-running task has no effect, leading
to resource exhaustion and inability to shut down gracefully.

# Mitigation

Pass a `threading.Event` to each task and check `event.is_set()`
periodically inside the task loop.

# Non-compliant

```python
from concurrent.futures import ThreadPoolExecutor
import time

def take_time(x):
    for i in range(10):
        time.sleep(1)

with ThreadPoolExecutor() as executor:
    future = executor.submit(take_time, "A")
    future.cancel()  # Returns False if already running
```

# Compliant

```python
from concurrent.futures import ThreadPoolExecutor
from threading import Event
import time

def take_time(x, event):
    for _ in range(10):
        if event.is_set():
            return  # Save partial results
        time.sleep(1)

with ThreadPoolExecutor() as executor:
    e = Event()
    future = executor.submit(take_time, "A", e)
    future.cancel()
    e.set()  # Signals running task to stop
```

# Examples

See [examples/pyscg-0024/](examples/pyscg-0024/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 7](https://github.com/ossf/secure-coding-guide-for-python)
