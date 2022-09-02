---
order: 50
label: Finding the names of your compute nodes
icon: dot
---

The hostnames of compute nodes usually follow a sequential order (e.g. node01, node02, node03… node10). 

Users can find the names of their compute nodes by using the `nodeattr` command with a group; e.g.

- `nodeattr -s group`
    - shows a space-separated list of compute node hostnames with the gender "group"<br><br>
- `nodeattr -c group`
    - shows a comma-separated list of compute node hostnames with the gender "group"<br><br>
- `nodeattr -n group`
    - shows a new-line-separated list of compute node hostnames with the gender "group"

In order to make use of these commands you must already have created a gender and assigned nodes to it. The next page covers how to do this.