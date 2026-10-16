---
type: Secure Coding Rule
title: Specify Locale Explicitly
description: Compare locale-independent representations, not locale-formatted strings, to avoid environment-dependent bugs.
tags: [locale, encoding, comparison]
---

# Risk

Locale-dependent operations (date names, number formats, case conversion)
produce different results across environments, causing security bypasses or
logic errors when comparing strings formatted under different locales.

# Mitigation

Use locale-independent representations (e.g. `dt.month` integer) for
comparisons; set locale explicitly if locale-dependent output is required.

# Non-compliant

```python
import datetime
import locale

dt = datetime.datetime(2022, 3, 9)
locale.setlocale(locale.LC_ALL, 'en_IE.utf8')
currmonth = dt.strftime("%B")  # "March"
locale.setlocale(locale.LC_ALL, 'uk_UA.utf8')
othermonth = dt.strftime("%B")  # "березень"
assert currmonth == othermonth  # False — comparison fails
```

# Compliant

```python
import datetime
import locale

dt = datetime.datetime(2022, 3, 9)
locale.setlocale(locale.LC_ALL, 'en_IE.utf8')
currmonth = dt.month  # 3
locale.setlocale(locale.LC_ALL, 'uk_UA.utf8')
othermonth = dt.month  # 3
assert currmonth == othermonth  # True — locale-independent
```

# Examples

See [examples/pyscg-0043/](examples/pyscg-0043/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 2](https://github.com/ossf/secure-coding-guide-for-python)
