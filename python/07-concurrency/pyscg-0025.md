---
type: Secure Coding Rule
title: Configure Adequate Resource Pools
description: Use a bounded ThreadPoolExecutor instead of spawning a thread per message, to prevent resource-exhaustion DoS.
tags: [concurrency, thread-pool, denial-of-service, resource-exhaustion]
---

# Risk

Thread-per-message patterns allow a single client to exhaust CPU/memory via
unbounded thread creation, enabling DoS.

# Mitigation

Use `ThreadPoolExecutor` with bounded `max_workers` and a timeout on
`wait()`, canceling incomplete futures.

# Non-compliant

```python
import threading

def process(msg):
    time.sleep(int(msg) * 0.01)

for msg in attacker_messages:
    threading.Thread(target=process, args=(msg,)).start()
```

# Compliant

```python
from concurrent.futures import ThreadPoolExecutor, wait

executor = ThreadPoolExecutor()
futures = [executor.submit(process, m) for m in messages]
done, not_done = wait(futures, timeout=1)
for f in not_done:
    f.cancel()
```

# Examples

See [examples/pyscg-0025/](examples/pyscg-0025/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 7](https://github.com/ossf/secure-coding-guide-for-python)
