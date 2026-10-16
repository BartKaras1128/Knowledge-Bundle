---
type: Secure Coding Rule
title: Ensure Thread Pool Tasks Do Not Fail Silently
description: Always check future.result() or future.exception() for submitted tasks; ThreadPoolExecutor otherwise swallows exceptions silently.
tags: [concurrency, thread-pool, error-handling, silent-failure]
---

# Risk

`ThreadPoolExecutor` suppresses task exceptions; without calling
`future.result()` or `future.exception()`, errors go unnoticed and bugs
hide.

# Mitigation

Always check `future.result()` or `future.exception()` for submitted tasks;
handle exceptions from `map()` iterators.

# Non-compliant

```python
from concurrent.futures import ThreadPoolExecutor
import math

with ThreadPoolExecutor() as executor:
    future = executor.submit(math.sqrt, -1)
    # ValueError silently swallowed, never observed
```

# Compliant

```python
from concurrent.futures import ThreadPoolExecutor
import math

with ThreadPoolExecutor() as executor:
    future = executor.submit(math.sqrt, -1)
    if future.exception() is not None:
        raise ValueError(f"Task failed: {future.exception()}")
    result = future.result()
```

# Examples

See [examples/pyscg-0030/](examples/pyscg-0030/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 7](https://github.com/ossf/secure-coding-guide-for-python)
