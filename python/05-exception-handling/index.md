---
okf_version: "0.1"
---

# Chapter 5 — Exception Handling

Improper exception handling leads to information disclosure, resource
leaks, and denial of service.

# Rules

* [pyscg-0014 — Use Specific Exception Types](pyscg-0014.md) - raise the most specific matching exception
* [pyscg-0015 — Handle Error Conditions](pyscg-0015.md) - wrap file I/O in try/except on OSError
* [pyscg-0016 — Propagate Exceptions and Preserve Context](pyscg-0016.md) - never use bare except
* [pyscg-0018 — Validate Numeric Data Beyond Type Checking](pyscg-0018.md) - use math.isnan/isfinite, not equality
* [pyscg-0028 — Preserve Exceptions in Finally Blocks](pyscg-0028.md) - no return/break/continue in finally
* [pyscg-0052 — Ensure Cleanup on Exceptions](pyscg-0052.md) - use with statements for guaranteed cleanup
