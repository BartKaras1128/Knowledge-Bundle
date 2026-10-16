---
type: Secure Coding Rule
title: Prevent OS Command Injection
description: Avoid concatenating user input into shell commands; use list-arg subprocess calls or pathlib instead of shell=True.
tags: [injection, command-injection, subprocess, rce]
---

# Risk

Concatenating user input into shell commands allows RCE via `;`, `&`, `|`.

# Mitigation

Use `pathlib`/`shutil`; if subprocess is unavoidable, use list args with
`shell=False`.

# Non-compliant

```python
Popen("ls " + dirname, shell=True).communicate()
```

# Compliant

```python
from pathlib import Path
path = Path(allowed / dirname).resolve()
path.relative_to(allowed.resolve())  # raises on traversal
for item in Path(dirname).glob("*"):
    print(item)
```

# Examples

See [examples/pyscg-0009/](examples/pyscg-0009/).

# Related

See also [pyscg-0044 — Canonicalize Input Before Validating](../02-encoding/pyscg-0044.md),
since Unicode bypass can defeat path validation used to prevent this class of injection.

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 4](https://github.com/ossf/secure-coding-guide-for-python)
