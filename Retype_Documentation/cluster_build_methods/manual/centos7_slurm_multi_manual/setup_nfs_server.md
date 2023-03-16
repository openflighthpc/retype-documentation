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
    systemctl start nfs
    systemctl enable nfs
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


## Testing

If all was successful, then the following should be the case on the head node:

1. The `export` directory exists, and contains these four directories:
    ```
    [root@chead1 ~]# ls /export/
    apps  data  service  site
    ```

2. The `export` directory has these permissions:
    ```
    [root@chead1 ~]# ls -l /export
    total 0
    drwxrwxr-x. 2 root root 6 Sep 20 09:36 apps
    drwxrwxr-x. 2 root root 6 Sep 20 09:36 data
    drwxrwxr-x. 2 root root 6 Sep 20 09:36 service
    drwxrwxr-x. 2 root root 6 Sep 20 09:36 site
    ```

3. The files `/etc/exports` and `/etc/fstab` both contain the information from the instructions.

4. The `opt` directory exists, and contains these four directories:
    ```
    [root@chead1 ~]# ls /opt/
    apps  data  service  site
    ```

5. The command `systemctl status nfs` shows the service as active with no errors.

6. The command `showmount --exports` displays that the correct directories have been exported, e.g.

    ```
    [root@chead1 ~]# showmount --exports
    Export list for chead1.pri.mycluster1.cluster.local:
    /home           10.50.0.0/16
    /export/site    10.50.0.0/16
    /export/service 10.50.0.0/16
    /export/data    10.50.0.0/16
    /export/apps    10.50.0.0/16
    ```
