---
type: Secure Coding Rule
title: Prevent SQL Injection
description: Use parameterized queries; never build SQL with string formatting or executescript() on untrusted data.
tags: [injection, sql-injection, database]
---

# Risk

SQL built with f-strings/`.format()` lets attackers drop tables or extract
data.

# Mitigation

Parameterized queries with `?` placeholders; never `executescript()` with
user data.

# Non-compliant

```python
query = "INSERT INTO Students VALUES('{name}');".format(name=name)
self.cursor.executescript(query)
```

# Compliant

```python
self.cursor.execute("INSERT INTO Students VALUES (?)", (name,))
```

# Examples

See [examples/pyscg-0010/](examples/pyscg-0010/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 4](https://github.com/ossf/secure-coding-guide-for-python)
