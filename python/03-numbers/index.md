---
okf_version: "0.1"
---

# Chapter 3 — Numbers

Numeric handling in Python introduces precision loss, overflow, and
comparison pitfalls, especially when mixing built-in types with fixed-width
C-backed types (numpy, datetime, math).

# Rules

* [pyscg-0001 — Control Numeric Precision](pyscg-0001.md) - use Decimal for money, not float
* [pyscg-0002 — Guard Fixed-Width Numbers Against Overflow](pyscg-0002.md) - validate bounds on numpy/timedelta/math
* [pyscg-0003 — Use Arithmetic Over Bitwise Operations](pyscg-0003.md) - avoid shift/precedence traps
* [pyscg-0004 — Use Integer Loop Counters](pyscg-0004.md) - avoid float accumulation errors
* [pyscg-0005 — Specify Rounding for Numeric Conversions](pyscg-0005.md) - explicit rounding mode for financial math
* [pyscg-0006 — Use an Appropriate Comparator for Numbers](pyscg-0006.md) - never compare stringified floats
* [pyscg-0007 — Use String Literals for Decimal Construction](pyscg-0007.md) - `Decimal("0.45")` not `Decimal(0.45)`
