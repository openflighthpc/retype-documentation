---
order: 80
label: Install Repositories
icon: dot-fill
---

Some repositories will be needed later to install Flight tools.


On **all** nodes do:

```bash
yum install epel-release -y
```

!!!
`-y` is an option for the install command that answers yes to install confirmation messages. 
!!!


Once this command has been run on **every** node, the cluster is ready for the next step.