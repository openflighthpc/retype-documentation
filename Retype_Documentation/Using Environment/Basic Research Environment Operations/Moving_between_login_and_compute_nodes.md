---
order: 0

---
OpenFlight Compute research environments automatically configure a trust relationship between login and compute nodes in the same research environment to allow users to login between nodes via SSH without a password. This configuration allows moving quickly and easily between nodes, and simplifies running large-scale jobs that involve multiple nodes. From the command line, a user can simply use the `ssh <node-name>` command to login to one of the compute nodes from the login node. For example, to login to a compute node named `node01` from the login node, use the command:

`ssh node01`

Use the command `logout` or `exit` (or press **CTRL**+**D**) to exit the compute node and return to the login node.

