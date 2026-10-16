---
okf_version: "0.1"
---

# Chapter 1 — Process Isolation & Trust Zones

Foundational secure coding principles: isolating trust zones at the OS level,
externalizing secrets from source code, avoiding obfuscated operator
precedence that hides logic errors, and enforcing access control server-side.

# Rules

* [pyscg-0040 — Use Process Isolation for Trust Zones](pyscg-0040.md) - separate OS users per trust zone
* [pyscg-0041 — Externalize Configuration and Secrets](pyscg-0041.md) - no hardcoded credentials in source
* [pyscg-0042 — Ensure Correct Operator Precedence](pyscg-0042.md) - avoid obfuscated bitwise logic
* [pyscg-0055 — Determine Access on Server Side](pyscg-0055.md) - never trust client-supplied identity/role
