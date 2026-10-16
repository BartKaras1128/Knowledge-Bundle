---
type: Secure Coding Rule
title: Exclude Developer Tools From the Final Product
description: Never ship monkey patches, debug=True, or print-based debugging to production.
tags: [debug-mode, developer-tools, attack-surface]
---

# Risk

Debug tooling (monkey patches, open debug ports, verbose logging) in
production expands the attack surface. CVE-2018-14649 scored CVSS 9.8 from
Flask debug mode left enabled (CWE-489).

# Mitigation

Keep debug tooling in separate packages; never ship monkey patches,
`debug=True`, or print-based debugging to production.

# Non-compliant

```python
def patched_process_payment(self, amount):
    print(f"DEBUG: Payment amount: {amount}, state: {self.__dict__}")
    logging.debug("Full payment details: %s", self.__dict__)
    return True

# Monkey patch left in production
PaymentProcessor.process_payment = patched_process_payment
```

# Compliant

```python
import logging
logger = logging.getLogger(__name__)

class PaymentProcessor:
    def process_payment(self, amount):
        logger.info("Processing payment of %s", amount)
        return True
```

# Examples

See [examples/pyscg-0021/](examples/pyscg-0021/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 6](https://github.com/ossf/secure-coding-guide-for-python)
