---
order: 50
label: '3\. Configuring a Multinode Cluster With Flight Profile'
icon: dot
---

Now that a login node and one or more compute nodes have been launched according the the instructions of the previous page, the cluster is ready to be configured.


1. [Log in](/general_environment_usage/cli_basics/logging_in/) to the login node.

2. [Become the root user](/general_environment_usage/cli_basics/becoming_the_root_user/).

## Parse Nodes

3. Parse your nodes with the command `flight hunter parse`. 
    This will generate a list, for example:
    ```
    [flight@login-node.novalocal ~]$ flight hunter parse
    Select nodes: (Scroll for more nodes)
    ‣ ⬡ login-node.novalocal - 127.0.0.1
      ⬡ compute-node-1.novalocal - 10.151.15.194
      ⬡ compute-node-2.novalocal - 10.151.15.238
    ```
    Begin by parsing your login node. Select it from the list with `space`, and you will be taken to the label editor.

    ```
    Choose label: login-node.novalocal
    ```
    Here, you can edit the label like plain text.
    ```
    Choose label: login1
    ```
    When done editing, press `enter` to save. The modified node label will appear next to the ip address and original node label.
    ```
    Select nodes: login-node.novalocal - 127.0.0.1 (login1) (Scroll for more nodes)
    ‣ ⬢ login-node.novalocal - 127.0.0.1 (login1)
      ⬡ compute-node-1.novalocal - 10.151.15.194
      ⬡ compute-node-2.novalocal - 10.151.15.238
    ```
    From this point, you can either hit `enter` to finish parsing and process the selected nodes, or continue changing nodes. Either way, you can return to this list by running `flight hunter parse`. 

    Parse all the nodes you intend to have in your cluster before moving on to the next step.

    !!!
    See `flight hunter parse -h` for more ways to parse nodes.
    !!!

## Add genders

5. **Optionally**, you may add genders to the newly parsed nodes. For example, in the case that the login node should have the gender `login` and `all` then I would run the command:
    ```
    flight hunter modify-groups --add login,all login1
    ```
    The other nodes can also have genders, e.g. giving the other nodes the gender `nodes` and `all`
    ```
    flight hunter modify-groups --add nodes,all node01
    flight hunter modify-groups --add nodes,all node02
    ```
    !!!
    if you have a lot of compute nodes, you can group them all faster with regex, e.g. the above might be:
    ```
    flight hunter modify-groups --add nodes,all --regex node0*
    ```
    !!!
    

## Apply Profiles

+++ Slurm

6. Configure profile

    ```
    flight profile configure
    ```
    This brings up a UI, where several options need to be set. Use up and down arrow keys to scroll through options and enter to move to the next option. Options in brackets coloured yellow are the default options that will be applied if nothing is entered.
    - Cluster type: The type of cluster setup needed, in this case `Slurm Multinode`.
    - Cluster name: The name of the cluster.
    - NFS server: The hostname or flight-hunter label of the node that will act as the NFS server.
    - SLURM server: The hostname or flight-hunter label of the node that will act as the SLURM server.
    - Default user: The user that you log in with.
    - Set user password: Set a password to be used for the chosen default user.
    - IP or FQDN for Web Access: As described [here](/hpc_environment_usage/flight_web_suite/installation_and_setup/configuring_web_suite/#setting-domain-name), this could be the public IP or public hostname.
    - IP range of compute nodes: The IP range of the compute nodes used, remember to add the netmask. E.g. `172.31.16.0/20`
    - Create hosts entries from Flight Hunter data: Flight profile can create /etc/hosts file entries based on the data it automatically collects on connected nodes.
    
7. Apply identities by running the command `flight profile apply`
    a. First apply an identity to the login node. E.g. 
    ```
    flight profile apply login1 login
    ```
    b. Wait for the login node identity to finish applying. You can check the status of all nodes with `flight profile list`.
    c. Apply an identity to the each of the compute nodes.  E.g.
    ```
    flight profile apply node01,node02 compute
    ```
    !!! 
    You can check all available identities for the current profile with `flight profile identities`
    !!!

8. Once all the identities have been applied, the cluster is ready to go.

+++ Kubernetes

6. Configure profile

    ```
    flight profile configure
    ```
    This brings up a UI, where several options need to be set. Use up and down arrow keys to scroll through options and enter to move to the next option. Options in brackets coloured yellow are the default options that will be applied if nothing is entered.
    - Cluster type: The type of cluster setup needed, in this case `Openflight Kubernetes Multinode`.
    - Cluster name: The name of the cluster.
    - Default user: The user that you log in with.
    - IP range of compute nodes: The IP range of the compute nodes used, remember to add the netmask. E.g. `172.31.16.0/20`
    - Create hosts entries from Flight Hunter data: Flight profile can create /etc/hosts file entries based on the data it automatically collects on connected nodes, this is recommended.
    
7. Apply identities by running the command `flight profile apply`
    a. First apply an identity to the login node. E.g. 
    ```
    flight profile apply login1 login
    ```
    b. Wait for the login node identity to finish applying. You can check the status of all nodes with `flight profile list`.
    c. Apply an identity to the each of the compute nodes.  E.g.
    ```
    flight profile apply node01,node02 compute
    ```
    !!! 
    You can check all available identities for the current profile with `flight profile identities`
    !!!

8. Once all the identities have been applied, the cluster is ready to go.

+++

