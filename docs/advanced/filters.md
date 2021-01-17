# Custom Filters
Nauti has the functionality to filter origin and target sources through custom python plugins. Nauti enables filtering though using an `Auditor` decorator that exposes several functions to filter origin and target collections.

To create a custom filter create a `plugins` folder within the `nauti` configuration directory and create a python containing the custom Auditor classes.

## Auditor
When a custom filter has been declared by using the Auditor class decorator it is automatically imported into the Nauti project there are also functions that can be used to easily filter devices.

### Register
The register decorator can accept four values:

| Key | Description | Required |
| --- | --- | --- |
| **origin** | The origin application to apply the filter to. | True |
|**target** | The target application to apply the filter to. | True |
| **collection** | The collection the filter is to be applied. | True |
| **name** | A custom name for the filter | False |

For the filter to be applied the CLI command must match the order in which the custom filter is configured.

For example the following python code would match
```python
from nauti.auditor import Auditor

@Auditor.register('ipfabric', 'netbox', 'devices')
class IPF2NBDevices(Auditor):
```

```shell
$ nauti sync --origin ipfabric --target netbox --collection devices
```

The class requires two values to be defined within `fields` and `key_fields`. Both variables require a list/tuple, these values are the fields and keys to filter on from the collections.

```python
@Auditor.register('ipfabric', 'netbox', 'devices')
class IPF2NBDevicesAuditor(Auditor):

    fields = ['hostname', 'os_name']
    key = ('hostname',)
```

### Functions
There are a number of functions that are available within the class that can be overwritten to inject custom filter logic.

| Function | Description |
| --- | --- |
| origin_fetch_filter | Returns a source specific fetch filter for the origin source |
| origin_key_filter | Returns bool if the given item fields should be included in the key formation |
| target_fetch_filter | Returns a source specific fetch filter for the target source |
| target_key_filter | Return bool if the given item fields should be included in the key formation |

#### Fetch Filter
A fetch filter is a source specific filter for the origin/target source. For example the `nauti-netbox` source will take a JSON payload to apply to the Netbox API call.

```json
{
    'platform__n': 'null',
    'has_primary_ip': 'true'
}
```

This JSON payload will be applied to the Netbox API calls and will only show devices with a platform and primary IP address configured.

The key filter allows python logic to be applied and filter out key values. Item is passed into the function which contains a single collection item. To filter out a collection item simply return False and to match a collection item return True.

```python
@Auditor.register('ipfabric', 'netbox', 'devices')
class IPF2NBDevicesAuditor(Auditor):

    fields = ['hostname', 'os_name']
    key = ('hostname',)

    def origin_key_filter(self, item: dict) -> bool:
        if item['os_name'] == 'junos':
            return False

        return True
```

This example will filter out IPFabric devices that have the `os_name` of `junos` by returning `False` and allow everything else by returning `True`.

## Output
Using the following configuration:

```python
@Auditor.register('ipfabric', 'netbox', 'devices')
class IPF2NBDevicesAuditor(Auditor):

    fields = ['hostname', 'os_name']
    key = ('hostname',)

    def origin_key_filter(self, item: dict) -> bool:
        if item['os_name'] == 'junos':
            return False

        return True
```

The following output shows that only the non junos platforms will be added Netbox.

```shell
$ nauti sync --origin ipfabric --target netbox --collection devices --diff-report add
2021-01-17 00:43:12,170 INFO: Fetching ipfabric/devices collection ...
2021-01-17 00:43:12,189 INFO: Fetched ipfabric/devices, fetched 16 records.
2021-01-17 00:43:12,190 INFO: Fetching netbox/devices collection ...
2021-01-17 00:43:13,578 INFO: Fetched netbox/devices, fetched 628 records.

Diff Report
   Add items: count 2
   Remove items: count 478
   Update items: count 0


--------------------------------------------------------------------------------
Add Items: 2
--------------------------------------------------------------------------------

sn           hostname        ipaddr         site        os_name    vendor    model
-----------  --------------  -------------  ----------  ---------  --------  -----------
1234         nexus-switch-b  192.168.3.144  Axians Lab  nx-os      cisco     N5K-C5548UP
1234         nexus-switch-a  192.168.3.143  Axians Lab  nx-os      cisco     N5K-C5548UP
```
