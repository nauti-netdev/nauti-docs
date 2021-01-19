# NAUTI ClearPass

Aruba ClearPass is a policy management platform that allows for network access control.

## NAUTI Collection Model Compatibility

| Name | Fetch | Add | Update | Delete |
| --- | --- | --- | --- | --- |
| devices | :material-check: | :material-close: | :material-close: | :material-close: |

## Configuration

As mentioned within [Architecture](../architecture.md) the `nauti-clearpass` package requires a configuration file to function correctly. Environment variables can be used to hide credentials.

```toml
[clearpass.default]
    url = "$CLEARPASS_ADDR"
    credentials.client_id = "$CLEARPASS_CLIENT_ID"
    credentials.client_secret = "$CLEARPASS_CLIENT_SECRET"
    options.timeout = 60

[clearpass.vars]
    tacacs_secret = "$TACACS_SECRET"
```

---

**Source Code**: <a href="https://github.com/nauti-netdev/nauti-clearpass" target="_blank">https://github.com/nauti-netdev/nauti-clearpass</a>

---
