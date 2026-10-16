---
okf_version: "0.1"
---

# Chapter 7 — Concurrency

Secure use of Python's `threading`, `concurrent.futures`, `multiprocessing`,
and `asyncio` modules. Race conditions, deadlocks, thread-pool exhaustion,
silent task failures, and stale thread-local state are the primary risks.

# Rules

* [pyscg-0024 — Ensure Thread Pool Tasks Can Be Interrupted](pyscg-0024.md) - use threading.Event, not future.cancel()
* [pyscg-0025 — Configure Adequate Resource Pools](pyscg-0025.md) - bounded ThreadPoolExecutor, not per-message threads
* [pyscg-0026 — Prevent Deadlocks](pyscg-0026.md) - never nest submit() on the same bounded pool
* [pyscg-0027 — Prevent Race Conditions](pyscg-0027.md) - lock compound read-modify-write on shared state
* [pyscg-0029 — Reinitialize Reused Thread Objects](pyscg-0029.md) - reset thread-local state per task
* [pyscg-0030 — Ensure Thread Pool Tasks Do Not Fail Silently](pyscg-0030.md) - always check future.result()/exception()
