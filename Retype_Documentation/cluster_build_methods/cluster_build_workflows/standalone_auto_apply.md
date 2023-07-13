---
order: 80
label: 'Automatic Slurm on Openstack' 
icon: dot-fill
---




### Overview
This workflow demonstrates the creation of a standalone slurm cluster on Openstack which utilises Flight Solo to automatically configure the node upon boot. It is assumed that you have a flight solo image on openstack, if not see the documentation [here](/cluster_build_methods/get_flight_solo/openstack_setup_solo/).


### Prepare Network

Preparing the network, router and subnet is out of scope for this documentation, so it is assumed that this is already done. See the [Openstack documentation](https://docs.openstack.org/install-guide/launch-instance.html#create-virtual-networks) for more information.

Create a Security Group with:
- Name: autostandalone1-sg
- Description: "Security group for automatic standalone cluster"

Ingress Rules:
- "SSH",  remote: "CIDR", CIDR: "`0.0.0.0/0`"
- "HTTP",  remote: "CIDR", CIDR: "`0.0.0.0/0`"
- "HTTPS",  remote: "CIDR", CIDR: "`0.0.0.0/0`"
- "All TCP", remote: "Security Group",  from this security group
- "All UDP", remote: "Security Group",  from this security group

Create a keypair with:
- Key Pair Name: autostandalone-key
- Key Type: SSH Key



### Launch the instance

- Click Launch Instance.
- Details:
    - Instance Name: `auto-slurm`
    - Count: `1`
- Source:
    - Volume Size: `20`
    - Image: imported Flight Solo image
- Flavour: `m1.medium`
- Networks: your network
- Configuration
    - Customisation script:
    ```
    #cloud-config
    write_files:
    - content: |
        LABEL="standalone1"
        AUTOPARSEMATCH="auto"
        PROFILE_ANSWERS='{"cluster_type": "openflight-slurm-standalone",  "cluster_name": "my-cluster",  "default_username": "flight",  "default_password": "0penfl1ght"}'
        AUTOAPPLY="standalone: all-in-one" 
      path: /opt/flight/cloudinit.in
      permissions: '0644'
      owner: root:root
    users:
      - default  
    ```
Press Launch Instance

Wait for the node to finish building, and associate it with a floating ip from the node's drop down menu.

### Checking it works


Congratulations! You now have a Slurm Standalone Cluster!

Once the node has come up it will automatically configure and set up the slurm profile on itself (see `flight profile list` ), with no more human interaction required before it is ready to run jobs.

What you can do next is:
- Seamlessly access the cluster via the Flight Web Suite in a web browser by visiting the Floating IP you assigned it.
- Run some slurm jobs.