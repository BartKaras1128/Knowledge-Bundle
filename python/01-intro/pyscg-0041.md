---
type: Secure Coding Rule
title: Externalize Configuration and Secrets
description: Load credentials from protected config or a secrets manager at deploy time instead of hardcoding them in source.
tags: [secrets, credentials, configuration]
---

# Risk

Hardcoded credentials can be extracted from source, `.pyc` files, or packages;
they cannot be rotated at runtime and may violate HIPAA/GDPR/CCPA.

# Mitigation

Load secrets from protected config files (`chmod 0o400`) or a secrets manager
at deployment time; use certificate-based auth over passwords.

# Non-compliant

```python
def front_end():
    server_config = {}
    server_config["IP"] = "192.168.0.1"
    server_config["PORT"] = "8080"
    server_config["USER"] = "admin"
    server_config["PASS"] = "SuperSecret123"
    logging.debug("connecting to server PASS %s", server_config["PASS"])
```

# Compliant

```python
def front_end(config_file_path: Path):
    _config = configparser.ConfigParser()
    _config.read(config_file_path)
    logging.debug("connecting to server IP %s", _config["SERVER"]["IP"])
    logging.debug("connecting to server pem %s", _config["SERVER"]["CERT_FILE"])
# Config file created at deploy time with chmod 0o400
# Certificate-based auth replaces password
```

# Examples

See [examples/pyscg-0041/](examples/pyscg-0041/).

# Related

See also [pyscg-0019 — Exclude Sensitive Data From Logs](../06-logging/pyscg-0019.md), which
covers the same non-compliant snippet's secondary problem (logging the password).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 1](https://github.com/ossf/secure-coding-guide-for-python)
