---
order: 100
label: 'Kubernetes on AWS' 
icon: dot-fill
---


*with Automatic Worker Node Building*


### Overview
This workflow demonstrates the creation of a multinode Kubernetes cluster on AWS which utilises Flight Solo to automatically configure nodes as workers in the Kubernetes cluster upon boot.

### Prepare Network

Create a VPC with:
- Name: kubecluster1

In "VPC and More":
- IPv4 Subnet Block: 10.10.0.0/16
- Number of Availability Zones: 1
- Public Subnets: 1
- Private Subnets: 0
- VPC Endpoints: None


Create a Security Group with:
- Name: kubecluster1-sg
- Description: "Security group for kubecluster1 cluster"
- VPC: <the kubecluster1 VPC just created>

Inbound Rules:
- "SSH" from "Anywhere-IPv4"
- "HTTP" from "Anywhere-IPv4"
- "HTTPS" from "Anywhere-IPv4"
- "All Traffic" from 10.10.0.0/16


### Build Login Node

Launch the Flight Solo image in AWS marketplace
- Select "Launch from EC2"
- Instance Type: t2.2xlarge
- Click "Edit" on Network Settings and
- VPC: kubecluster1
- Auto-assign public IP: Enable
- Select existing security group: kubecluster1-sg
- Set root volume size to at least 20GB
- Under Advanced Details -> User Data, add this:
    ```
    #cloud-config
    write_files:
      - content: |
          SHAREPUBKEY="true"
          AUTOPARSEMATCH=".*"
          AUTH_KEY=kubecluster1
        path: /opt/flight/cloudinit.in
        permissions: '0644'
        owner: root:root
    ```
!!!
The above data will enable sharing the public key to clients, automatically add any nodes that
connect to hunter with a correct auth key, and secure node hunting with the authorisation key of kubecluster1
!!!

### Configure Login Node

Parse & Label Login Node
- Run the command `flight hunter parse`.
- Select the node with space.
- Press the down arrow key to erase the field.
- Type in login1 as the label and press enter.

### Configure Kubernetes & Setup Login Node

Login to node as the flight user.

Run flight profile configure and Select `OpenFlight Kubernetes Multinode`

- Cluster Name: kubecluster1
- Default user: flight
- Set user password to: Some secure password
- NFS server (hostname or flight-hunter label): login1
- IP or FQDN for Web Access: Public IPv4 DNS from AWS EC2 Console for Node
- IP Range of Compute Nodes: 10.10.0.0/16
- IP Range of Kubernetes Pods (must not overlap with Compute Node IP Range): 192.168.0.0/16


Apply the master profile to login1 with `flight profile apply login1 master`

Wait for flight profile list to show the status of login1 as completed

### Setup Automatic Application of Hunter Nodes
Add the following lines to `/opt/flight/opt/hunter/etc/config.yml` to automatically apply the worker profile to hunter nodes with labels containing `node`.
```
auto_apply:
  node: worker
```
!!!
You will need to use sudo to have permissions to edit this config file.
!!!

Restart hunter service
`flight service restart hunter`

### Launch a Compute Node

Launch the Flight Solo image in AWS marketplace

Select "Launch from EC2"
- Instance Type: t2.2xlarge

Click "Edit" on Network Settings and select:
- VPC: kubecluster1
- Auto-assign public IP: Disable
- Select existing security group: kubecluster1-sg

Set root volume size to at least 20GB

Under Advanced Details -> User Data (replace `LOGIN_SERVER_IPV4_PRIVATE_ADDRESS` with
the IP of the login node, this can be found with ip addr on that system):


    #cloud-config
    write_files:
      - content: |
          SERVER=<LOGIN_SERVER_IPV4_PRIVATE_ADDRESS>
          LABEL=node01
          AUTH_KEY=kubecluster1
        path: /opt/flight/cloudinit.in
        permissions: '0644'
        owner: root:root

Repeat the above to create more nodes, changing the `LABEL=` field in the cloud-init data to be a
unique label.

### Checking it Works
Congratulations! You now have an automatically expanding Kubernetes cluster!

Once the compute node has come up it will be automatically added to the accepted list of hosts for
the cluster (see `flight hunter list` ) and will have the Kubernetes worker profile applied to it
automatically (see `flight profile list` ).

What you can do next is:
- Seamlessly access the cluster via the Flight Web Suite in a web browser by visiting the Public IPv4 DNS from AWS EC2 Console for the login node
- Run some kubernetes pods
- Add more nodes as described in the [Launch a Compute Node](/cluster_build_methods/cluster_build_workflows/kubernetes_on_aws/#launch-a-compute-node) section
- Remove unused nodes from the cluster before deleting them from AWS