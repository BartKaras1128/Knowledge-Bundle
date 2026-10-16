---
type: Secure Coding Rule
title: Determine Access on Server Side
description: Never trust client-supplied identity or role fields; resolve session identity server-side.
tags: [authorization, access-control, session]
---

# Risk

Accepting user identity or role from client-supplied form data (CWE-472)
allows privilege escalation via browser tools or intercepting proxies.

# Mitigation

Manage session state server-side using session cookies, validated JWTs, or
an IdAM solution (e.g. OIDC); never trust client-supplied identity fields.

# Non-compliant

```python
def post(self, form_data):
    action = form_data.get("action", "")
    session_user = form_data.get("session_user", "")  # client-controlled!
    if session_user not in self.users:
        return form_data, "401: Please login"
    action_data = self._submit(session_user, action)
    return form_data, action_data
```

# Compliant

```python
# session_user resolved server-side from validated session token/JWT
# NOT from form_data or any client-supplied field
# Role lookup via server-side RBAC after authentication
def post(self, request):
    session_user = self.get_authenticated_user(request.session_token)
    if not session_user:
        return "401: Please login"
    return self._submit(session_user, request.action)
```

# Examples

See [examples/pyscg-0055/](examples/pyscg-0055/).

# Citations

[1] [OpenSSF Secure Coding Guide for Python — Chapter 1](https://github.com/ossf/secure-coding-guide-for-python)
