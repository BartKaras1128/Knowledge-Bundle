---
type: Secure Coding Rule
title: Use Allow Lists Over Deny Lists
description: Reject everything except known-safe values instead of trying to enumerate everything unsafe.
tags: [allow-list, deny-list, xss, validation]
---

# Risk

Deny lists are incomplete — `<script生>` bypasses naive blacklists, enabling
XSS.

# Mitigation

Allow-list only known-safe values; reject everything else.

# Non-compliant

```python
if tag in ["<script>", "<img", "<a href"]:
    raise ValueError("Invalid")  # <script生> bypasses
```

# Compliant

```python
if tag not in ["<b>", "<p>", "</p>"]:
    raise ValueError("Invalid input tag")
```

# Examples

See [examples/pyscg-0047/](examples/pyscg-0047/).

# Related

See also [pyscg-0045 — Enforce Consistent Encoding](../02-encoding/pyscg-0045.md), which
covers the same `<script生>` bypass pattern from the encoding-conversion angle.

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 4](https://github.com/ossf/secure-coding-guide-for-python)
