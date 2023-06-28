---
order: 90
label: User Data
icon: dot-fill
---

User data, cloud init data or cloud data is a way of giving data to an instance for it to run as part of the startup process. This page will describe how to craft a cloud init script to suit your cluster.


### Basic multinode setup
This script would be given to the compute nodes of a multinode cluster to make setup easy. It allows the login node to find the compute nodes as long as they are on the same network, and ssh into them from the root user (which is necessary for setup). 
```
#cloud-config
users:
  - default    
  - name: root
    ssh_authorized_keys:
      - <Content of ~/.ssh/id_alcescluster.pub from root user on login node>
```

One thing to note is that with this data all nodes on the network will pick up the compute node being launched, so other users could hijack your compute node.


### Cloud config options

- `SERVER=<local ip of server>` - Sets the ip address that this node will send to, and does a `send` on startup to the ip address. This is where `flight hunter send` will go if no ip address argument is provided. *(conflicts with `BROADCAST_ADDRESS`)*
- `BROADCAST_ADDRESS=<ip range>` - The node will broadcast its information across an ip range. *(conflicts with `SERVER`)*
- `AUTH_KEY=<password>` - Sets an auth key that is used by `flight hunter hunt` and `flight hunter send`.
- `LABEL=<nodename>` - Sets label to be sent with flight hunter.
- `PREFIX=<nodeprefix>` - Sets prefix for flight hunter send.
- `AUTOPARSEMATCH=<node>` - Sets the regex for auto-parse rules in the hunter server. It also makes the hunter server automatically parse hunted nodes. *(must be passed to your login node)*
!!!
Note that `AUTOPARSEMATCH` looks at the hostname of a node, even if the node was passed with a `LABEL`.
!!!
- `SHAREPUBKEY=true` - If set to true then this node will share the root user’s pub ssh key over network on port 1234. This means that any solo images with `SERVER` set to this node will attempt to grab its public key.
- `PROFILE_ANSWERS=<json string>` - Set to json text which is used to answer [profile configure](/flight_environment_usage/flight_tools/flight_profile/#configure) questions, the format should be the same as for the profile configure sub-option [`--answers`](/flight_environment_usage/flight_tools/flight_profile/#configure). Any answers not supplied will be set to their default values.
- `AUTOAPPLY="<regex>: <identity>, <regex>: <identity>"` - Set automatic application of identities to nodes. When a node connects with hunter, if it matches one of the regular expressions then the corresponding identity will be applied. 
!!!
`AUTOAPPLY` can only start if a cluster type has already been configured on this node.
!!!
- `PREFIX_STARTS="<regex>: '<start number>', <regex>: '<start number>'"` - Set prefix start numbers based on node name. When a node connects with hunter, if it matches one of the regular expressions then it will be given a number, starting with the start number and incrementing until there is an unused number.

!!!
Many of these relate to command line options that are explained in more detail in the [hunter documentation](/flight_environment_usage/flight_tools/flight_hunter/).
!!!


``` An example of all mentioned lines in a single cloud init script. 
#cloud-config
write_files:
  - content: |
      SERVER=10.50.0.43
      BROADCAST_ADDRESS=10.50.255.255
      AUTH_KEY=banana
      LABEL=<nodename>
      PREFIX=<nodeprefix>
      AUTOPARSEMATCH=<node>
      SHAREPUBKEY=true
      PROFILE_ANSWERS='{"cluster_type": "openflight-slurm-standalone",  "cluster_name": "my-cluster",  "default_username": "flight",  "default_password": "0penfl1ght",  "access_host": "10.151.15.51"}''
      AUTOAPPLY="node: compute, controller: login" 
      PREFIX_STARTS="node: '01', gpu: '1'"
    path: /opt/flight/cloudinit.in
    permissions: '0644'
    owner: root:root
users:
  - default    
  - name: root
    ssh_authorized_keys:
      - <Content of ~/.ssh/id_alcescluster.pub from root user on login node>
```

!!!
Note that in the above example `SERVER` and `BROADCAST_ADDRESS` are both present to display correct formatting. Only the first of these lines will have an effect because they are mutually exclusive. 
!!!


