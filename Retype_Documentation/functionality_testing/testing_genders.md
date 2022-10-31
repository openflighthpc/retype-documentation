---
order: 50
label: Genders and PDSH
icon: dot-fill
---

Genders and PDSH grant a way to control multiple nodes at once. As such it will not function on a single node environment. To test its functionality:


1. Show a space separated list of all the nodes with the gender `<gender>`.
    ```
    nodeattr -s <gender>
    ```
    

2. Execute the uptime command on all nodes of the gender `<gender>`
    ```
    pdsh -g <gender> uptime
    ```
    This should show the time since last boot for each node.



### More Information

All information about Genders and PDSH can be found the dedicated [documentation section](/general_environment_usage/genders_and_pdsh/finding_the_names_of_your_compute_nodes/).
