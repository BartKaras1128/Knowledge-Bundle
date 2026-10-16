---
type: Secure Coding Rule
title: Prevent Format String Injection
description: Never let untrusted input become a format string template; use string.Template instead.
tags: [injection, format-string, information-disclosure]
---

# Risk

User-controlled format strings leak globals via
`{0.__init__.__globals__[SECRET]}`.

# Mitigation

Use `string.Template`; never let user input become the format template.

# Non-compliant

```python
message_format = MESSAGE + customer
print(message_format.format(mc))  # leaks __globals__
```

# Compliant

```python
from string import Template
MSG = Template("Contract '$instance_name' for '$customer'")
print(MSG.substitute(instance_name=mc.name, customer=customer))
```

# Examples

See [examples/pyscg-0008/](examples/pyscg-0008/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 4](https://github.com/ossf/secure-coding-guide-for-python)
