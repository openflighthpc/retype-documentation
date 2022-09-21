---
order: 80
label: Install Repositories
icon: dot
---

Some repositories will be needed later to install Flight tools.


1. On **all** nodes do:

	```bash
	dnf install -y epel-release
	```

    !!!
    `-y` is an option for the install command that answers yes to install confirmation messages. 
    !!!


Once this command has been run on **every** node, the cluster is ready for the next step.

## Testing

If all was successful, the added repositories will appear when running the command `dnf repolist` on every node. E.g. on head node:

```
[root@chead1 ~]# dnf repolist
repo id            repo name
appstream          CentOS Stream 8 - AppStream
baseos             CentOS Stream 8 - BaseOS
epel               Extra Packages for Enterprise Linux 8 - x86_64
epel-modular       Extra Packages for Enterprise Linux Modular 8 - x86_64
extras             CentOS Stream 8 - Extras
```