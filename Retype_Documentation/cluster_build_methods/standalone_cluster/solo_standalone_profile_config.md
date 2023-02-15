---
order: 40
label: '2\. Configuring a Standalone Cluster with Flight Profile'
icon: dot
---


A standalone cluster runs on just one instance, create one before going through these instructions.


1. [Log in](/general_environment_usage/cli_basics/logging_in/) to the node.

2. [Become the root user](/general_environment_usage/cli_basics/becoming_the_root_user/).


## Parse Node

3. Parse your node with the command `flight hunter parse`. 
    This will generate a list, for example:
    ```
    [flight@standalone-login-node.novalocal ~]$ flight hunter parse
    Select nodes: (Scroll for more nodes)
    ‣ ⬡ standalone-login-node.novalocal - 127.0.0.1
    ```
    The standalone node will likely be the only one on the list. Select it with `space`, and you will be taken to the label editor.

    ```
    Choose label: standalone-login-node.novalocal
    ```
    Here, you can edit the label like plain text.
    ```
    Choose label: standalone1
    ```
    !!!
    You can clear the current node name by pressing down in the label editor.
    !!!
    When done editing, press `enter` to save. The modified node label will appear next to the ip address and original node label.
    ```
    Select nodes: standalone-login-node.novalocal - 127.0.0.1 (standalone1) (Scroll for more nodes)
    ‣ ⬢ standalone-login-node.novalocal - 127.0.0.1 (standalone1)
    ```
    From this point, you can either hit `enter` to finish parsing and process the selected nodes, or continue changing nodes. Either way, you can return to this list by running `flight hunter parse`. 

    Save the standalone node before moving on to the next step.

    !!!
    See `flight hunter parse -h` for more ways to parse nodes.
    !!!


## Add genders

4. **Optionally**, you may add genders to the newly parsed node. For example, in the case that the node should have the gender `standalone` and `all` then I would run the command:
    ```
    flight hunter modify-groups --add standalone,all standalone1
    ```

## Apply Profile

+++ Slurm

5. Configure profile

    ```
    flight profile configure
    ```
    
    This brings up a UI, where several options need to be set. Use up and down arrow keys to scroll through options and enter to move to the next option. Options in brackets coloured yellow are the default options that will be applied if nothing is entered.
    - Cluster type: The type of cluster setup needed, in this case select `Slurm Standalone`.
    - Cluster name: The name of the cluster.
    - Default user: The user that you log in with.
    - Set user password: Set a password to be used for the chosen default user.
    - IP or FQDN for Web Access: As described [here](/flight_environment_usage/flight_web_suite/installation_and_setup/configuring_web_suite/#setting-domain-name), this could be the public IP or public hostname.
    
6. Apply an identity by running the command `flight profile apply`, E.g. 
    ```
    flight profile apply standalone1 all-in-one
    ```
    !!! 
    You can check all available identities for the current profile with `flight profile identities`
    !!!
7. Wait for the identity to finish applying. You can check the status of all nodes with `flight profile list`.

+++
