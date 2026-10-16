---
okf_version: "0.1"
---

# Chapter 4 — Neutralization (Injection Prevention)

Improper neutralization — untrusted input reaching commands, queries, format
strings, or serialized data without sanitization. Consistently among the most
exploited classes (OWASP Top 10, CWE Top 25).

# Rules

* [pyscg-0008 — Prevent Format String Injection](pyscg-0008.md) - never let user input become the format template
* [pyscg-0009 — Prevent OS Command Injection](pyscg-0009.md) - avoid shell=True with concatenated input
* [pyscg-0010 — Prevent SQL Injection](pyscg-0010.md) - parameterized queries, never string-built SQL
* [pyscg-0011 — Prevent Type Confusion](pyscg-0011.md) - cast external inputs at trust boundaries
* [pyscg-0012 — Extract Archives Safely](pyscg-0012.md) - guard against zip slip and zip bombs
* [pyscg-0013 — Secure Search Paths](pyscg-0013.md) - isolate against PYTHONPATH/bytecode injection
* [pyscg-0023 — Secure Deserialization](pyscg-0023.md) - never pickle.loads() untrusted data
* [pyscg-0047 — Use Allow Lists Over Deny Lists](pyscg-0047.md) - allow-list known-safe values
