# NAUTI NetBox

![NetBox](../images/netbox_logo.svg)

NetBox is an IP address management (IPAM) and data center infrastructure management (DCIM) tool. NAUTI Netbox can be used as either an `Origin` or `Target`.

## NAUTI Collection Model Compatibility

| Name | Fetch | Add | Update | Delete |
| --- | --- | --- | --- | --- |
| devices | :material-check: | :material-check: | :material-check: | :material-close: |
| interfaces | :material-check: | :material-check: | :material-check: | :material-close: |
| ipaddrs | :material-check: | :material-check: | :material-close: | :material-close: |
| portchans | :material-check: | :material-check: | :material-check: | :material-check: |
| sites | :material-check: | :material-check: | :material-close: | :material-close: |

## Configuration

As mentioned within [Architecture](../architecture.md) the `nauti-netbox` package requires a configuration file to function correctly. Environment variables can be used to hide credentials.

```toml
[netbox.default]
    url = "$NETBOX_ADDR"
    credentials.token = "$NETBOX_TOKEN"
    options.timeout = 60
```

## Filtering

`nauti-netbox` supports API filtering using the Netbox Rest API filtering technique. Information regarding the filters can be found within the [Netbox documentation](https://netbox.readthedocs.io/en/stable/rest-api/filtering/).

---

**Source Code**: <a href="https://github.com/nauti-netdev/nauti-netbox" target="_blank">https://github.com/nauti-netdev/nauti-netbox</a>

---
