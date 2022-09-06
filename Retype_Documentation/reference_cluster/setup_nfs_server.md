---
order: 70
label: Setup NFS Server
icon: dot-fill
---

On the head node, do:

```bash
yum install -y nfs-utils
```

Stay on the head node, and make a directory for everything that we may want to share.


```bash
mkdir /export
```
```bash
mkdir /export/{apps,data,service,site}
```
Then ensure that permissions are correct.

```bash
chmod 775 -R /export/
```

Go to `/etc/exports` and add this:


```
/export/apps 10.50.0.0/16(rw,no_root_squash,sync)
/export/data 10.50.0.0/16(rw,no_root_squash,sync)
/export/service 10.50.0.0/16(rw,no_root_squash,sync)
/export/site 10.50.0.0/16(rw,no_root_squash,sync)
/home 10.50.0.0/16(rw,no_root_squash,sync)
```

Now we need to bind mounts for the NFS server.


Open the the file `/etc/fstab` and add this:

```
/export/apps /opt/apps none defaults,bind 0 0
/export/data /opt/data none defaults,bind 0 0
/export/service /opt/service none defaults,bind 0 0
/export/site /opt/site none defaults,bind 0 0
/home /home none defaults,bind 0 0
```

Save and close the file.

Create several new directories:

```bash
mkdir /opt/{apps,data,service,site}
```

Then start and enable NFS:
```bash
systemctl start nfs
```
```bash
systemctl enable nfs
```
!!!
`start` activates NFS, and `enable` means that NFS will startup on boot.
!!!


```bash
exportfs -va
```
(v for verbose, a for all)

```bash
mount -a
```

At this point, the NFS server has now been setup. 
