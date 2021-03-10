# Welcome to NAUTI

NAUTI (Network Automation Tools Integrator) is a CLI application that leverages an ecosystem of libraries built around asyncio that together can be used to support various network automation workflows.

The key features include:

- **Compare**: The ability to compare network automation tools
- **Reconcile**: NAUTI can be used to reconcile information between network automation tools
- **Diffs**: Show differences between network automation tools

## Quick Overview

Within this quick example the CLI can be used to sync devices from [IPFabric](https://ipfabric.io/) (Network Discovery Tool) to [Netbox](https://github.com/netbox-community/netbox) (Network DCIM/IPAM).

The following command checks if there are any differences between the origin and target filtering out only one device. By default the command line `nauti sync` will run in `dry-run` mode.
```bash
$ nauti sync --origin ipfabric --target netbox --collection devices --origin-filter "hostname ~ b15"
2021-01-04 19:16:57,473 INFO: Fetching ipfabric/devices collection ...
2021-01-04 19:16:57,489 INFO: Fetched ipfabric/devices, fetched 1 records.
2021-01-04 19:16:57,489 INFO: Fetching netbox/devices collection ...
2021-01-04 19:16:58,690 INFO: Fetched netbox/devices, fetched 627 records.

Diff Report
   Add items: count 0
   Remove items: count 477
   Update items: count 1
```

You can show a more detailed output by adding the `--diff-report/--dr` command line argument.
```bash
$ nauti sync --origin ipfabric --target netbox --collection devices --origin-filter "hostname ~ b15" --diff-report upd
2021-01-04 19:20:44,276 INFO: Fetching ipfabric/devices collection ...
2021-01-04 19:20:44,300 INFO: Fetched ipfabric/devices, fetched 1 records.
2021-01-04 19:20:44,300 INFO: Fetching netbox/devices collection ...
2021-01-04 19:20:45,821 INFO: Fetched netbox/devices, fetched 627 records.

Diff Report
   Add items: count 0
   Remove items: count 477
   Update items: count 1


--------------------------------------------------------------------------------
Update Items: 1
--------------------------------------------------------------------------------

sn            hostname             ipaddr        site         os_name    vendor    model       status
------------  -------------------  ------------  -----------  ---------  --------  ----------  --------
BP1234567123  tor-mgmt-ex4200-b15  192.168.3.35  Axians--lab  junos      juniper   ex4200      active
              ex4200-b15                         Axians Lab                        ex4200-48t
```

## Requirements

Python 3.8+

## License

This project is licensed under the terms of the [GNU General Public License v3.0](https://www.gnu.org/licenses/gpl-3.0.en.html).
