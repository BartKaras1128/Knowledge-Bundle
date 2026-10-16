---
type: Secure Coding Rule
title: Release Unused Resources
description: Use with statements for all resource access; explicitly clear collections that hold resource references.
tags: [resource-cleanup, file-handles, denial-of-service]
---

# Risk

Unreleased file handles, sockets, or connections accumulate and exhaust OS
limits, causing denial of service in long-running processes.

# Mitigation

Use `with` statements for all resource access; explicitly close/release
when `with` isn't feasible; clear collections holding resource references.

# Non-compliant

```python
my_list = []
def append_resource(name):
    resource = {"name": name, "active": True}
    my_list.append(resource)

append_resource("A")
append_resource("B")
# Resources never released
```

# Compliant

```python
my_list = []
append_resource("A")
append_resource("B")

for resource in my_list:
    resource["active"] = False
my_list.clear()
```

# Examples

See [examples/pyscg-0051/](examples/pyscg-0051/).

# Related

See also [pyscg-0052 — Ensure Cleanup on Exceptions](../05-exception-handling/pyscg-0052.md)
and [pyscg-0035 — Complete Resource Cleanup](pyscg-0035.md).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 8](https://github.com/ossf/secure-coding-guide-for-python)
