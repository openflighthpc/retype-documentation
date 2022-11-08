---
order: 60
label: (AWS) Configuring a Multinode Cluster With Flight Solo
icon: dot
---

Now that a login node and one or more compute nodes have been launched according the the instructions of the previous page, the cluster is ready to be configured.


1. [Log in](/general_environment_usage/cli_basics/logging_in/) to the login node.

## Parse Nodes

2. Parse the login node with the command `flight hunter parse`. 
    - Add the option `--prefix <name>` to set a name for every selected login node.
    - Add the option `--start <number>` to add a number to every login node name, that increments with each one.
    - For example:
        ```
        flight hunter parse --prefix login --start 1
        ```

    This will generate a list, for example:
    ```
    [flight@ip-172-31-19-83 ~]$ flight hunter parse --prefix login --start 1
    Select the nodes that you wish to save: (Scroll for more nodes)
    ‣ ⬡ ip-172-31-19-83.eu-west-2.compute.internal (127.0.0.1)
      ⬡ ip-172-31-27-136.eu-west-2.compute.internal (172.31.27.136)
      ⬡ ip-172-31-34-31.eu-west-2.compute.internal (172.31.34.31)
    ```
    Select all the nodes that need to be set as a login node, they can be identified by their name or ip address. In most cases this will be just the local node. 
    !!!
    Scroll the list with the up and down arrow keys, select a node by pressing space, and confirm with the enter key.
    !!!


3. Parse the compute nodes with the command `flight hunter parse`.
    - Add the option `--prefix <name>` to set a name for every selected compute node.
    - Add the option `--start <number>` to add a number to every compute node name, that increments with each one.
    - For example:
        ```
        flight hunter parse --prefix node --start 01
        ```

    This will generate a list, for example:
    ```
    [flight@ip-172-31-19-83 ~]$ flight hunter parse --prefix node --start 01
    Select the nodes that you wish to save: (Scroll for more nodes)
    ‣ ⬡ ip-172-31-27-136.eu-west-2.compute.internal (172.31.27.136)
      ⬡ ip-172-31-34-31.eu-west-2.compute.internal (172.31.34.31)
    ```
    Select all the nodes that need to be set as a compute node, they can be identified by their name or ip address. Note that the login node is no longer visible since it was selected earlier.

    !!!
    Scroll the list with the up and down arrow keys, select a node by pressing space, and confirm with the enter key.
    !!!

## Add genders

4. (OPTIONALLY) Optionally, you may add genders to the newly parsed nodes. For example, in the case that the login node should have the gender `login` and `all` then I would run the command:
    ```
    flight hunter modify-groups --add login,all login1
    ```
    The other nodes can also have genders, e.g. giving the other nodes the gender `nodes` and `all`
    ```
    flight hunter modify-groups --add nodes,all node01
    flight hunter modify-groups --add nodes,all node02
    ```

## Apply Profiles

5. Configure profile

    ```
    flight profile configure
    ```
    This brings up a UI, where several options need to be set. Use up and down arrow keys to scroll through options and enter to move to the next option. Options in brackets coloured yellow are the default options that will be applied if nothing is entered.
    - Cluster type: The type of cluster setup needed.
    - Cluster name: The name of the cluster.
    - NFS server: The hostname or flight-hunter label of the node that will act as the NFS server.
    - SLURM server: The hostname or flight-hunter label of the node that will act as the SLURM server.
    - Default user: The user that you log in with.
    - Set user password: Set a password to be used for the chosen default user.
    - IP or FQDN for Web Access: the IP or FQDN used to access the Flight Web Suite.
    - IP range of compute nodes: The IP range of the compute nodes used. NETMASK
    - Create hosts entries from Flight Hunter data: Flight profile can create /etc/hosts file entries based on the data it automatically collects on connected nodes.
    
6. Build profiles by running the command `flight profile apply`
    E.g. applying the login profile to a login node, and the compute profile to compute nodes
    ```
    flight profile apply login1 login
    flight profile apply node01,node02 compute
    ```

7. Once the profiles have been applied, the cluster is ready to go. Check the status of profile application with the command `flight profile list`.

