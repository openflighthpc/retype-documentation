---
order: 60
label: Setup NFS Clients
icon: dot
---

The NFS server has been setup on the head node, now every other node must be set up as an NFS client.


1. Install NFS
	```bash
	yum install -y nfs-utils
	```

2. Open the file `/etc/fstab` and add the following text, then save and exit.
	```
	chead1:/export/apps    /opt/apps     nfs    intr,rsize=32768,wsize=32768,vers=3,_netdev,nofail    0 0
	chead1:/export/data    /opt/data     nfs    intr,rsize=32768,wsize=32768,vers=3,_netdev,nofail    0 0
	chead1:/export/service /opt/service  nfs    intr,rsize=32768,wsize=32768,vers=3,_netdev,nofail    0 0
	chead1:/export/site    /opt/site     nfs    intr,rsize=32768,wsize=32768,vers=3,_netdev,nofail    0 0
	chead1:/home           /home         nfs    intr,rsize=32768,wsize=32768,vers=3,_netdev,nofail    0 0
	```

3. Make directories for NFS:
	```bash
	mkdir /opt/{apps,data,service,site}
	```

4. Start NFS
	```bash
	systemctl start nfs
	systemctl enable nfs
	```

5. Mount NFS
	```bash
	mount -a
	```

At this point, this node is fully setup to be an NFS client. Repeat these steps on every other node (except the head node), and then NFS will be completely set up.


## Testing

If all was successful, then the following should be the case on all compute nodes:

1. The file `/etc/fstab` should contain the information from the instructions.

2. The `opt` directory exists, and contains these four directories:
    ```
    [root@cnode01 ~]# ls /opt
    apps  data  service  site
    ```

3. The command `systemctl status nfs` shows the service as active with no errors.

4. The command `df -h` shows that NFS has been successfully mounted. E.g.
	```
	[root@cnode01 ~]# df -h
	Filesystem              Size  Used Avail Use% Mounted on
	devtmpfs                872M     0  872M   0% /dev
	tmpfs                   907M     0  907M   0% /dev/shm
	tmpfs                   907M  8.5M  898M   1% /run
	tmpfs                   907M     0  907M   0% /sys/fs/cgroup
	/dev/vda1                10G  1.6G  8.5G  16% /
	tmpfs                   182M     0  182M   0% /run/user/0
	chead1:/export/apps      10G  1.6G  8.5G  16% /opt/apps
	chead1:/export/data      10G  1.6G  8.5G  16% /opt/data
	chead1:/export/service   10G  1.6G  8.5G  16% /opt/service
	chead1:/export/site      10G  1.6G  8.5G  16% /opt/site
	chead1:/home             10G  1.6G  8.5G  16% /home
	```