---
order: 70
label: Setup NFS Server
icon: dot
---

The instructions on this page are done entirely on the head node.

1. On the head node, do:

	```bash
    yum install -y nfs-utils
	```

2. Make a directory for everything that we may want to share.

	```bash
    mkdir /export
    mkdir /export/{apps,data,service,site}
	```
3. Ensure that permissions are correct.

	```bash
    chmod 775 -R /export/
	```

4. Go to `/etc/exports` and add this:


	```
    /export/apps 10.50.0.0/16(rw,no_root_squash,sync)
    /export/data 10.50.0.0/16(rw,no_root_squash,sync)
    /export/service 10.50.0.0/16(rw,no_root_squash,sync)
    /export/site 10.50.0.0/16(rw,no_root_squash,sync)
    /home 10.50.0.0/16(rw,no_root_squash,sync)
	```

5. Bind mounts for the NFS server. Open the the file `/etc/fstab` and add this, then save and close the file.

	```
    /export/apps    /opt/apps none defaults,bind 0 0
    /export/data    /opt/data none defaults,bind 0 0
    /export/service /opt/service none defaults,bind 0 0
    /export/site    /opt/site none defaults,bind 0 0
	```

6. Create several new directories:

	```bash
    mkdir /opt/{apps,data,service,site}
	```

7. Start and enable NFS:
	```bash
    systemctl start nfs-server.service
    systemctl enable nfs-server.service
	```
	!!!
    `start` activates NFS, and `enable` means that NFS will startup on boot.
	!!!



8. Export and show the mount points, then mount them.
	```bash
    exportfs -va
    mount -a
	```
	!!!
	the v option shows more information and the a option exports/mounts all.
	!!!

The NFS server has now been setup. 
