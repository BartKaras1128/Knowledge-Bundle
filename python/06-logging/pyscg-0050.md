---
type: Secure Coding Rule
title: Sanitize Error Output to Prevent Information Disclosure
description: Catch exceptions at trust boundaries and return only a generic error ID to the client; log full details server-side.
tags: [information-disclosure, error-handling, logging]
---

# Risk

Unfiltered exceptions expose internal paths, DB structure, usernames, and
system layout to attackers (CWE-209, CWE-497).

# Mitigation

Catch exceptions at trust boundaries; log full details server-side, return
only a generic error ID to the client.

# Non-compliant

```python
from pathlib import Path

class FileReader:
    def __init__(self, args: list[str]):
        path = Path(Path.home(), args[0])
        fh = open(path, 'r', encoding="utf-8")
        fh.readlines()
# Exposes: PermissionError: 'C:\Users\user1\Documents'
```

# Compliant

```python
import logging, random
from pathlib import Path

def file_reader(args: list):
    filepath = Path(Path.home(), args[0]).resolve()
    try:
        if Path.home() not in filepath.parents:
            raise PermissionError("Invalid file")
        _ = filepath.read_text(encoding='utf8')
    except (PermissionError, IsADirectoryError):
        error_id = f"{random.getrandbits(64):16x}"
        logging.exception("ERROR %s", error_id)
        print(f"ERROR {error_id}: Unable to retrieve file '{filepath.stem}'")
```

# Examples

See [examples/pyscg-0050/](examples/pyscg-0050/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 6](https://github.com/ossf/secure-coding-guide-for-python)
