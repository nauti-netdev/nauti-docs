# Architecture

NAUTI has three key components.

- NAUTI Core
- NAUTI Sources
- NAUTI Collections

### NAUTI Core

NAUTI Core is the core library which glues all of the other components together. The library contains the core functionality such as the CLI entrypoint and collection models.

### NAUTI Sources

NAUTI Sources define the Network Automation Tools in which NAUTI will use for gathering and reconciling information between systems. An example of a NAUTI Source could be [IPFabric](https://ipfabric.io), [NetBox](https://github.com/netbox-community/netbox) and many more.

Currently Implemented:

 - IPFabric
 - NetBox
 - ClearPass


###Configuration Parameters

NAUTI Sources require a configuration file. The configuration is typically `<nauti-source>.toml` such as `ipfabric.toml`. Each configuration can contain a number of parameters.

| Type | Description |
| --- | --- |
| default | Contains source information such as `url`, `credentials` and `options` |
| vars | Any variables to be passed to the source |
| expands | Expand items such as "Et" to "Ethernet" |
| maps | Maps one value to another value |

> Note: default `url` and `credentials` accepts environment variables to prevent storing sensitive information within plain text files.

`url`, `credentials` and `vars` supports using environment variables within the configuration:

```toml
[netbox.default]
    url = "$NETBOX_ADDR"
    credentials.token = "$NETBOX_TOKEN"
```

### NAUTI Collections

NAUTI Collections are components of a network that are similar between different tools. For example a collection can be defined as a Device, Interface, PortChannel, Site and more. Each collection type is modeled within NAUTI Core.

An example device data model contains the following:

- Hostname
- Serial Number
- IP Address
- Site
- OS Name
- Vendor
- Model

These collection models can be used within a NAUTI Source to gather information and translate it to the NAUTI Collection data model. This allows the data model to be used by a target NAUTI Source to add, update or delete records.

### Implemented Collection Models

| Name | Fields | Keys |
| --- | --- | --- |
| devices | sn, hostname, ipaddr, site, os_name, vendor, model | sn |
| interfaces | hostname, interface, description | hostname, interface |
| ipaddrs | hostname, ipaddr, interface | hostname, ipaddr |
| portchans | hostname, interface, portchan | hostname, interface |
| sites | name | name |

###Configuration Parameters

NAUTI Collections require a configuration file. The configuration is typically `<nauti-collection>.toml` such as `devices.toml`. This configuration can contain a number of parameters.

| Type | Description |
| --- | --- |
| name | Name of the collection |
| fields | Allows for the filtering of collection model fields |
| sources | Allows for additional settings to be passed into a collection for a specific source |
| options | Optional parameters to pass into a collection |
