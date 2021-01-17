# NAUTI IPFabric

![IPFabric](../images/IPFabricLogoOnly.png)

IPFabric helps companies discover, verify, visualize and document large scale networks within minutes. Due to the nature of IPFabric dynamically discovering devices and information about a network it is only used within NAUTI as an `Origin`.

## NAUTI Collection Model Compatibility

| Name | Fetch | Add | Update | Delete |
| --- | --- | --- | --- | --- |
| devices | :material-check: | :material-close: | :material-close: | :material-close: |
| interfaces | :material-check: | :material-close: | :material-close: | :material-check: |
| ipaddrs | :material-check: | :material-close: | :material-close: | :material-close: |
| portchans | :material-check: | :material-close: | :material-close: | :material-close: |
| sites | :material-check: | :material-close: | :material-close: | :material-close: |

## Configuration
As mentioned within [Architecture](../architecture.md) the `nauti-ipfabric` package requires a configuration file to function correctly. Environment variables can be used to hide credentials.

```toml
[ipfabric.default]
    url = "$IPF_ADDR"
    credentials.token = "$IPF_TOKEN"


[ipfabric.expands.interface]

    # -------------------------------------------------------------------------
    # map IP Fabric "short interface name" to "long interface name"
    # ------------------------------------------------------------------------

    "Et" = "Ethernet"
    "Lo" = "Loopback"
    "Vl" = "Vlan"
    "Po" = "Port-Channel"
    "Gi" = "GigabitEthernet"
    "Te" = "TenGigabitEthernet"
    "Vx" = "VxLan"
```

---

**Source Code**: <a href="https://github.com/nauti-netdev/nauti-ipfabric" target="_blank">https://github.com/nauti-netdev/nauti-ipfabric</a>

---
