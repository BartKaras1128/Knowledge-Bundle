---
okf_version: "0.1"
---

# Chapter 6 — Logging

Logging is essential for debugging and incident response but introduces
security risks when sensitive data leaks into logs, untrusted input is
written unsanitized, or debug tooling ships to production.

# Rules

* [pyscg-0019 — Exclude Sensitive Data From Logs](pyscg-0019.md) - never log passwords/PII
* [pyscg-0020 — Implement Informative Event Logging](pyscg-0020.md) - audit trail for auth events
* [pyscg-0021 — Exclude Developer Tools From the Final Product](pyscg-0021.md) - no debug tooling in production
* [pyscg-0022 — Neutralize Untrusted Data in Logs](pyscg-0022.md) - allow-list input before logging
* [pyscg-0050 — Sanitize Error Output to Prevent Information Disclosure](pyscg-0050.md) - generic client errors, full details server-side
