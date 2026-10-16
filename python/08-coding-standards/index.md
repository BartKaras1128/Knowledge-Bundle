---
okf_version: "0.1"
---

# Chapter 8 — Coding Standards

Rules that prevent subtle logic bugs, resource leaks, and bypassed security
checks caused by Python language misuse: correct iteration, identity vs
equality, None handling, resource lifecycle, and assertion safety.

# Rules

* [pyscg-0031 — Use Copies When Modifying Iterables](pyscg-0031.md) - iterate over .copy(), not the live collection
* [pyscg-0032 — Avoid Redefining Built-in Functions or Standard Library Identifiers](pyscg-0032.md) - never shadow len/str/os
* [pyscg-0033 — Implement Comparisons by Value Rather Than Reference](pyscg-0033.md) - define __eq__ for value-comparable classes
* [pyscg-0034 — Check for None Values](pyscg-0034.md) - guard before dereferencing Optional values
* [pyscg-0035 — Complete Resource Cleanup](pyscg-0035.md) - use NamedTemporaryFile with `with`, not raw mkstemp
* [pyscg-0036 — Check Return Values](pyscg-0036.md) - assign str.replace()/find() results, check -1 sentinel
* [pyscg-0037 — Presume Assertions May Be Disabled In Production](pyscg-0037.md) - use if/raise for validation, not assert
* [pyscg-0051 — Release Unused Resources](pyscg-0051.md) - use `with` for files/sockets/connections
