# Architecture
NAUTI has three key components.

- NAUTI Core
- NAUTI Sources
- NAUTI Collections

### NAUTI Core
NAUTI Core is the core library which glues all of the other components together. The library contains the core functionaility such as the CLI entrypoint and collection models.

### NAUTI Sources
NAUTI Sources define the Network Automation Tools in which NAUTI will use for gathering and reconsiling information between systems. An example of a NAUTI Source could be [IPFabric](https://ipfabric.io), [NetBox](https://github.com/netbox-community/netbox) and many more.

Currently Implemented:

 - IPFabric
 - NetBox
 - ClearPass

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
