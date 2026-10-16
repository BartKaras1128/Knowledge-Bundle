---
type: Secure Coding Rule
title: Complete Resource Cleanup
description: Use tempfile.NamedTemporaryFile with a with statement for automatic cleanup instead of raw mkstemp().
tags: [temp-files, resource-cleanup, disk-exhaustion]
---

# Risk

Temporary files left on disk after script completion cause resource
exhaustion and potential information disclosure.

# Mitigation

Use `tempfile.NamedTemporaryFile()` with a `with` statement for automatic
cleanup; avoid raw `mkstemp()` without `os.remove()`.

# Non-compliant

```python
import os
from tempfile import mkstemp

fd, path = mkstemp()
with os.fdopen(fd, 'w') as f:
    f.write('TEST\n')
# path never deleted
```

# Compliant

```python
import tempfile

with tempfile.NamedTemporaryFile() as temp_file:
    temp_file.write(b'Temporary data')
# File automatically deleted on exit
```

# Examples

See [examples/pyscg-0035/](examples/pyscg-0035/).

# Related

See also [pyscg-0051 — Release Unused Resources](pyscg-0051.md).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 8](https://github.com/ossf/secure-coding-guide-for-python)
