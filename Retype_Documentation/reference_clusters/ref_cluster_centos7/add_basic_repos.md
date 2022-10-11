---
order: 80
label: Install Repositories
icon: dot
---

Some repositories will be needed later to install Flight tools.


1. On **all** nodes do:

	```bash
	yum install -y epel-release
	```

    !!!
    `-y` is an option for the install command that answers yes to install confirmation messages. 
    !!!


Once this command has been run on **every** node, the cluster is ready for the next step.


## Testing

If all was successful, the added repositories will appear when running the command `yum repolist` on every node. E.g. on head node:

```
[root@chead1 ~]# yum repolist
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirror.freethought-internet.co.uk
 * epel: epel.mirror.liteserver.nl
 * extras: repo.uk.bigstepcloud.com
 * updates: mirror.mhd.uk.as44574.net
repo id                      repo name                                                  status
base/7/x86_64                CentOS-7 - Base                                            10,072
epel/x86_64                  Extra Packages for Enterprise Linux 7 - x86_64             13,750
extras/7/x86_64              CentOS-7 - Extras                                             516
updates/7/x86_64             CentOS-7 - Updates                                          4,160
repolist: 28,498
```