---
order: 40
label: Configuring a SLURM Standalone Cluster with Flight Profile
icon: dot-fill
---


A standalone cluster runs on just one instance, create one before going through these instructions.


1. [Log in](/general_environment_usage/cli_basics/logging_in/) to the node.

## Parse Node

2. Parse the node with the command `flight hunter parse`. 
    - Add the option `--prefix <name>` to set a name for every selected node.
    - Add the option `--start <number>` to add a number to every node name, that increments with each one.
    - For example:
        ```
        flight hunter parse --prefix standalone --start 1
        ```

    This will generate a list, for example:
    ```
    [flight@ip-172-31-19-83 ~]$ flight hunter parse --prefix standalone --start 1
    Select the nodes that you wish to save: (Scroll for more nodes)
    ‣ ⬡ ip-172-31-42-232.eu-west-2.compute.internal (172.31.42.232)
    ```
    Since this is a standalone cluster, there should only be one node in the list. 
    !!!
    Scroll the list with the up and down arrow keys, select a node by pressing space, and confirm with the enter key.
    !!!

## Add genders

3. **Optionally**, you may add genders to the newly parsed node. For example, in the case that the node should have the gender `standalone` and `all` then I would run the command:
    ```
    flight hunter modify-groups --add standalone,all standalone1
    ```

## Apply Profile

4. Configure profile

    ```
    flight profile configure
    ```
    
    This brings up a UI, where several options need to be set. Use up and down arrow keys to scroll through options and enter to move to the next option. Options in brackets coloured yellow are the default options that will be applied if nothing is entered.
    - Cluster type: The type of cluster setup needed, in this case select `Slurm Standalone`.
    - Cluster name: The name of the cluster.
    - Default user: The user that you log in with.
    - Set user password: Set a password to be used for the chosen default user.
    - IP or FQDN for Web Access: As described [here](/hpc_environment_usage/flight_web_suite/installation_and_setup/configuring_web_suite/#setting-domain-name), this could be the public IP or public hostname.
    
5. Apply an identity by running the command `flight profile apply`, E.g. 
    ```
    flight profile apply standalone1 all-in-one
    ```
    !!! 
    You can check all available identities for the current profile with `flight profile identities`
    !!!
6. Wait for the identity to finish applying. You can check the status of all nodes with `flight profile list`.


