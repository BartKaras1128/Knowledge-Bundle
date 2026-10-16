---
type: Secure Coding Rule
title: Enforce Consistent Encoding
description: Never silently strip characters from untrusted input during encoding conversion before security-relevant processing.
tags: [encoding, unicode, xss, data-loss]
---

# Risk

Changing encoding (e.g. UTF-8 to ASCII with `errors="ignore"`) can collapse
non-ASCII characters out of a payload, turning harmless strings like
`<script生>` into executable `<script>` tags.

# Mitigation

Use a single encoding (UTF-8) throughout the pipeline; never silently strip
characters from untrusted input before security-relevant processing.

# Non-compliant

```python
def read_message(message: bytes):
    # "ignore" silently drops non-ASCII bytes, collapsing
    # <script生> into <script>
    print(message.decode("ascii", "ignore"))

payload = "<script生>".encode("utf-8")
read_message(payload)  # Outputs: <script>
```

# Compliant

```python
import base64

def read_message(message: bytes):
    try:
        text = message.decode("utf-8")
    except UnicodeDecodeError:
        # Preserve data losslessly for forensic analysis
        text = base64.b64encode(message).decode("utf-8")
    print(text)

payload = "<script生>".encode("utf-8")
read_message(payload)  # Outputs: <script生>
```

# Examples

See [examples/pyscg-0045/](examples/pyscg-0045/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 2](https://github.com/ossf/secure-coding-guide-for-python)
