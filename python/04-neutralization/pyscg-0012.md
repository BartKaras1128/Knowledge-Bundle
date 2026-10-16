---
type: Secure Coding Rule
title: Extract Archives Safely
description: Validate every archive member's resolved path and actual byte size before extracting untrusted zip files.
tags: [zip-slip, zip-bomb, path-traversal, archive]
---

# Risk

Zip slip writes files outside the target directory via `../../`. Zip bombs
exhaust resources. Metadata can be forged.

# Mitigation

Resolve each path below the target, read actual bytes (don't trust
metadata), cap count/size.

# Non-compliant

```python
with zipfile.ZipFile("untrusted.zip") as archive:
    archive.extractall()  # no validation
```

# Compliant

```python
target = (base_path / item.filename).resolve()
if not str(target).startswith(str(base_path)):
    raise ValueError("Path traversal")
data = src.read(MAX_SIZE + 1)
if len(data) > MAX_SIZE:
    raise ValueError("Too large")
```

# Examples

See [examples/pyscg-0012/](examples/pyscg-0012/).

# Related

See also [pyscg-0044 — Canonicalize Input Before Validating](../02-encoding/pyscg-0044.md).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 4](https://github.com/ossf/secure-coding-guide-for-python)
