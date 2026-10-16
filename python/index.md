---
okf_version: "0.1"
---

# PYSCG Knowledge Bundle

OKF-formatted knowledge base for the OpenSSF Secure Coding Guide for Python
(PYSCG), used by the `local-crisp-python-secure-coding-reviewer-okf` agent.
Each of the 9 chapters groups a set of discrete rules; each rule is one
concept document with a non-compliant/compliant example pair and a link to
runnable example files.

# Chapters

* [Chapter 1 — Process Isolation & Trust Zones](01-intro/index.md) - OS-level trust boundaries, secrets, operator precedence, server-side access control
* [Chapter 2 — Encoding & Strings](02-encoding/index.md) - Locale, Unicode normalization, encoding consistency
* [Chapter 3 — Numbers](03-numbers/index.md) - Precision, overflow, rounding, numeric comparison
* [Chapter 4 — Neutralization (Injection)](04-neutralization/index.md) - Format string, OS command, SQL, deserialization, archive, allow-list injection
* [Chapter 5 — Exception Handling](05-exception-handling/index.md) - Exception specificity, error handling, NaN/infinity, finally blocks, cleanup
* [Chapter 6 — Logging](06-logging/index.md) - Sensitive data in logs, audit events, dev tooling, log injection, error disclosure
* [Chapter 7 — Concurrency](07-concurrency/index.md) - Thread pools, deadlocks, race conditions, thread-local state, silent failures
* [Chapter 8 — Coding Standards](08-coding-standards/index.md) - Iteration safety, shadowing, equality, None checks, resource cleanup, assertions
* [Chapter 9 — Cryptography](09-cryptography/index.md) - Cryptographically secure randomness

# Citations

[1] [OpenSSF Secure Coding Guide for Python](https://github.com/ossf/secure-coding-guide-for-python)
