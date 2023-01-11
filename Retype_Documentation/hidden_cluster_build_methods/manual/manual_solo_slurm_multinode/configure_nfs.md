---
order: 90
label: 'b\. Configure NFS'
icon: dot-fill
---


The next step is to setup NFS.

+++Login Node
On the login node:

1. Make a directory for everything that we may want to share.

	```bash
    mkdir /export
    mkdir /export/{apps,data,service,site}
	```
2. Ensure that permissions are correct.

	```bash
    chmod 775 -R /export/
	```

3. Go to `/etc/exports` and add this:

	```
    /export/apps 10.50.0.0/16(rw,no_root_squash,sync)
    /export/data 10.50.0.0/16(rw,no_root_squash,sync)
    /export/service 10.50.0.0/16(rw,no_root_squash,sync)
    /export/site 10.50.0.0/16(rw,no_root_squash,sync)
    /home 10.50.0.0/16(rw,no_root_squash,sync)
	```
    !!!
    The IP addresses and subnet mask you need to use will be different. 
    !!!

4. Bind mounts for the NFS server. Open the the file `/etc/fstab` and add this, then save and close the file.

	```
    /export/apps    /opt/apps none defaults,bind 0 0
    /export/data    /opt/data none defaults,bind 0 0
    /export/service /opt/service none defaults,bind 0 0
    /export/site    /opt/site none defaults,bind 0 0
	```

5. Create several new directories:

	```bash
    mkdir /opt/{apps,data,service,site}
	```

6. Start and enable NFS:
	```bash
    systemctl start nfs-server.service
    systemctl enable nfs-server.service
	```
	!!!
    `start` activates NFS, and `enable` means that NFS will startup on boot.
	!!!

7. Export and show the mount points, then mount them.
	```bash
    exportfs -va
    mount -a
	```
	!!!
	the `v` option shows more information and the `a` option exports/mounts all.
	!!!


The NFS server has now been setup. Follow the instructions on the compute nodes tab to complete setup.

+++ Compute Nodes

On a compute node:


1. Open the file `/etc/fstab` and add the following text, then save and exit.
	```
	chead1:/export/apps    /opt/apps     nfs    rsize=32768,wsize=32768,vers=3,_netdev,nofail    0 0
	chead1:/export/data    /opt/data     nfs    rsize=32768,wsize=32768,vers=3,_netdev,nofail    0 0
	chead1:/export/service /opt/service  nfs    rsize=32768,wsize=32768,vers=3,_netdev,nofail    0 0
	chead1:/export/site    /opt/site     nfs    rsize=32768,wsize=32768,vers=3,_netdev,nofail    0 0
	chead1:/home           /home         nfs    rsize=32768,wsize=32768,vers=3,_netdev,nofail    0 0
	```

2. Make directories for NFS:
	```bash
	mkdir /opt/{apps,data,service,site}
	```

3. Start NFS
	```bash
    systemctl start nfs-client.target
    systemctl enable nfs-client.target 

	```

4. Mount NFS
	```bash
	mount -a
	```

At this point, this node is fully setup to be an NFS client. Repeat these steps on every other compute node, and then NFS will be completely set up.

+++