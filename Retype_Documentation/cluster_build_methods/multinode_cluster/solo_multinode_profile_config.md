---
order: 50
label: '3\. Configuring a Multinode Cluster With Flight Profile'
icon: dot
---

Now that a login node and one or more compute nodes have been launched according the the instructions of the previous page, the cluster is ready to be configured.


1. [Log in](/general_environment_usage/cli_basics/logging_in/) to the login node.

2. [Become the root user](/general_environment_usage/cli_basics/becoming_the_root_user/).

## Parse Nodes

3. Parse the login node with the command `flight hunter parse`. 
    - Add the option `--prefix <name>` to set a name for every selected login node.
    - Add the option `--start <number>` to add a number to every login node name, that increments with each one.
    - For example:
        ```
        flight hunter parse --prefix login --start 1
        ```

    This will generate a list, for example:
    ```
    [root@chead1 ~]# flight hunter parse --prefix login --start 1
    Select the nodes that you wish to save: (Scroll for more nodes)
    ‣ ⬡ chead1.novalocal (10.50.0.13)
      ⬡ cnode01.novalocal (10.50.0.31)
      ⬡ cnode02.novalocal (10.50.0.26)
    ```
    Select the node that needs to be set as a login node, it can be identified by the name or ip address. *This should be the local node.*
    !!!
    Scroll the list with the up and down arrow keys, select a node by pressing space, and confirm with the enter key.
    !!!


4. Parse the compute nodes with the command `flight hunter parse`.
    - Add the option `--prefix <name>` to set a name for every selected compute node.
    - Add the option `--start <number>` to add a number to every compute node name, that increments with each one.
    - For example:
        ```
        flight hunter parse --prefix node --start 01
        ```

    This will generate a list, for example:
    ```
    [root@chead1 ~]# flight hunter parse --prefix node --start 01
    Select the nodes that you wish to save: (Scroll for more nodes)
    ‣ ⬡ cnode01.novalocal (10.50.0.31)
      ⬡ cnode02.novalocal (10.50.0.26)
    ```
    Select all the nodes that need to be set as a compute node, they can be identified by their name or ip address. *Note that the login node is no longer visible since it was selected earlier.*

    !!!
    Scroll the list with the up and down arrow keys, select a node by pressing space, and confirm with the enter key.
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

+++
