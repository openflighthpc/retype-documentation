---
icon: ":scream_cat:"
order: 0
---


There are multiple parameters in the template, some are required and others are optional, these are outlined below:

- `sourceimage` - The AMI ID to use for both the gateway and compute nodes

- `clustername` - The name of the cluster, to be used as part of the FQDN for nodes

- `customdata` - A base64 encoded cloudinit string for both the gateway and compute nodes

- `computeNodesCount` - The number of compute nodes to deploy, a value between 2 and 8 (default: 2)

- `gatewayinstancetype` - The instance type to be used for the gateway node (default: Standard DS1 v2)

- `computeinstancetype` - The instance type to be used for the compute nodes (default: Standard DS1 v2)

