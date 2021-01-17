# Installation
Installing NAUTI requires the installation of NAUTI Core and required NAUTI Sources.

## With pip

```bash
$ pip install git+https://github.com/nauti-netdev/nauti
$ pip install git+https://github.com/nauti-netdev/nauti-ipfabric
$ pip install git+https://github.com/nauti-netdev/nauti-netbox
```

## Configuration

NAUTI requires configuration file defined in TOML.

###Parameters
| Key | Type | Required | Description |
| --- | --- | --- | --- |
| domain_names: | List | False | Network Domain Names |
| sources | Dictionary | True | NAUTI Sources to use |
| collections | Dictionary | True | Collections to use |

Create the `nauti.toml` file.
```bash
$ vi nauti.toml
```

Define NAUTI Configuration
```toml
domain_names = []

sources = ['ipfabric', 'netbox']

collections = ['sites', 'devices']
```
