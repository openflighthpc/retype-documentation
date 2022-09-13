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


