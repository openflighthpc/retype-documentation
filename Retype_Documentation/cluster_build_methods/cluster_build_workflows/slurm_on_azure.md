---
order: 90
label: 'Slurm On Azure' 
icon: dot-fill
---

### Overview
This workflow demonstrates the creation of a multinode Slurm cluster on Microsoft Azure which utilises Flight Solo.

It is assumed that you have a flight solo image on azure, if not see the documentation [here](/cluster_build_methods/get_flight_solo/import_solo_azure/).


### Make a login node

1. Click on your image

2. Click create VM

3. On the Basics page:
    - Set *Subscription* to your subscription type.
    - Set *Resource Group* to your desired resource group (where the vm will be kept after creation). Alternatively, create a new resource group.
    - Set *Virtual machine name* to any suitable name. (`-` does not work in a name)
    - *Image* should be set to your Flight Solo Image.
    - Set *Size* to your choice of size.
    - Set *Authentication type* to `SSH public key`
    - Set *Username* to `flight`.
    - Set *SSH public key source* to the most suitable option, but remember what key was used if creating compute nodes later.
    - Fill in the *Key pair name/Stored key/Use existing key* as appropriate to the chosen public key source.
    - Set the most appropriate license type.

5. Go to the networking tab and fill out the necessary options.
    - Set *Virtual Network* or create a new one by pressing "Create new" and setting a name. **Remember what this is for if you create compute nodes.**
    - Set *Subnet* to one of the options in the dropdown menu, if it isn't already set. **Remember what this is for if you create compute nodes.**
    - Set *Public IP* to an existing public IP or create a new one by pressing "Create new" and setting a name.
    - Set *NIC network security group* to "Advanced", and press "Create new" to create a new security group.
        - Click on "Add an inbound rule" to open the inbound rule creator
        - Create rules to allow `HTTP`, `HTTPS` and `SSH` traffic from your IP address to the security group. Add a rule to allow traffic to port `8888` from your ip address with any protocol. *??? any ip address to hunter?* 
        - When complete, press "OK" at the bottom left of the screen to return to image creation.

6. Go to the *Advanced* tab and find the *custom data* box.
    - Copy in the following:
    ```
    #cloud-config
    write_files:
      - content: |
          AUTH_KEY=example
          PREFIX=login1
        path: /opt/flight/cloudinit.in
        permissions: '0644'
        owner: root:root
    ```

6. Skip to the final tab *Review + create*

7. Azure will take some time to review your settings. If there are no issues click "Create" to finish creation.


### Get information for Compute node setup

Login to the login node, then become the root user and get the contents of `~/.ssh/id_alcescluster.pub`.

### Create Compute node

Create another VM, filling it out with the same information as the login node but with these changes:
- Instead of creating a security group, use the security group created with the login node.
- Use this custom data:
    ```
    #cloud-config
    write_files:
    - content: |
        SERVER=<LOGIN_SERVER_IPV4_PRIVATE_ADDRESS>
        AUTH_KEY=example
        PREFIX=node0
      path: /opt/flight/cloudinit.in
      permissions: '0644'
      owner: root:root
    users:
    - default    
    - name: root
      ssh_authorized_keys:
        - <Content of ~/.ssh/id_alcescluster.pub from root user on login node>
    ```


### Parse Nodes

Login to the login node. 

Parse the nodes.
- Run the command `flight hunter parse`.
- Select a node with space.
- The prefix name will show up.
- Press enter to leave node editing.
- Repeat for each node in the list that is in your cluster
- Press enter from the list to finish.


### Configure Slurm 

Login to the login node.

Run flight profile configure and Select `OpenFlight Slurm Multinode`

- Cluster Name: slurmcluster1
- NFS server (hostname or flight-hunter label): login1
- SLURM server (hostname or flight-hunter label): login1
- Default user: flight
- Set user password to: <Some secure password>
- IP or FQDN for Web Access: <Public IPv4 DNS from AWS EC2 Console for Node>
- IP Range of Compute Nodes: 10.10.0.0/16
- IP Range of Kubernetes Pods (must not overlap with Compute Node IP Range): 192.168.0.0/16


Apply the login identity to login1 with `flight profile apply login1 login`

Wait for flight profile list to show the status of login1 as completed.

Apply the compute identity to your other node with `flight profile apply node0 compute`


Repeat the above to create more compute nodes.

### Checking it Works
Congratulations! You now have a Slurm cluster!

What you can do next is:
- Seamlessly access the cluster via the Flight Web Suite in a web browser by visiting the Public IPv4 DNS for the login node.
- Run some batch jobs.
- Add more nodes as described in the [Create a Compute Node](/cluster_build_methods/cluster_build_workflows/slurm_on_azure/#create-compute-node) section.
- Remove unused nodes from the cluster before deleting them from azure.