---
order: 70
label: Copying data between nodes
icon: dot-fill
---

Research environment login and compute nodes all mount the shared filesystem, so it is not normally necessary to copy data directly between nodes in the research environment. Users simply need to place the data to be shared in their home-directory on the login node, and it will be available on all compute nodes in the same location.

If necessary, users can use the `scp` command to copy files from the compute nodes to the login node; for example:

- `scp node01:/tmp/myfile.txt .`

Alternatively, users could login to the compute node (e.g. `ssh node01`) and copy the data back to the shared filesystem on the node:

```bash
ssh node01
cp /tmp/myfile ~/myfile
```
