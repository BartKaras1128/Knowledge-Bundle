---
okf_version: "0.1"
---

# Chapter 2 — Encoding & Strings

Encoding and string handling errors enable directory traversal, XSS, and data
corruption when programs mix encodings, compare locale-dependent strings, or
validate before canonicalizing.

# Rules

* [pyscg-0043 — Specify Locale Explicitly](pyscg-0043.md) - avoid locale-dependent comparison bugs
* [pyscg-0044 — Canonicalize Input Before Validating](pyscg-0044.md) - normalize before matching against patterns
* [pyscg-0045 — Enforce Consistent Encoding](pyscg-0045.md) - never collapse characters out of untrusted input
