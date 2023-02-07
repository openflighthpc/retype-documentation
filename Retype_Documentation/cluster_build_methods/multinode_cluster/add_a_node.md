---
order: 30
label: '5\. Adding a node to an existing cluster'
icon: dot
---

Sometimes, it may be necessary to add a node to a cluster after the cluster has already been created. This can be done with the following steps:


1. Create a new instance, following the steps to [create a compute node](/cluster_build_methods/multinode_cluster/make_compute_node/) on the same platform as the login instance.

!!!
Make sure that settings such as network, subnet, security group, user data, etc are all set correctly.
!!!

2. [Log in](/general_environment_usage/cli_basics/logging_in/) to the login node.

3. [Become the root user](/general_environment_usage/cli_basics/becoming_the_root_user/).

## Parse Node

4. Parse the newly created node with the command `flight hunter parse`. See [here](/cluster_build_methods/multinode_cluster/solo_multinode_profile_config/#parse-nodes) for more detailed information on parsing nodes. 


## Add genders

5. **Optionally**, you may add genders to the newly parsed node. For example, in the case of adding the node `newnode` to the group `all`:
    ```
    flight hunter modify-groups --add all newnode
    ```

6. Finally, apply an identity to the new node:

+++ Slurm
`flight profile apply newnode compute`
+++Kubernetes
`flight profile apply newnode worker`
+++


