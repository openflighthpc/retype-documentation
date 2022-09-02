---
order: 0
label: Using PDSH
icon: dot
---

Users can run a command across all compute nodes at once using the pdsh command. This can be useful if users want to make a change to all nodes in the research environment - for example, installing a new software package. The `pdsh` command can take a number of parameters that control how commands are processed; for example:

- `pdsh -g all uptime` 
    - executes the `uptime` command on all available compute and login nodes in the research environment<br><br>
- `pdsh -g nodes 'sudo yum -y install screen'`
    - use `yum` to install the `screen` package as the root user on all compute nodes<br><br>
- `pdsh -g nodes -f 1 df -h /tmp`
    - executes the command `df -h /tmp` on all compute nodes of the research environment, one at a time (fanout=1)<br><br>
- `pdsh -w node01,node03 which ldconfig`
    - runs the `which ldconfig` command on two named nodes only


To learn more about genders, read the [tutorial](https://github.com/chaos/genders/blob/master/TUTORIAL).