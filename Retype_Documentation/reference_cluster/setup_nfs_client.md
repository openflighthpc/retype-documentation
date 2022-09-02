---
order: 60
label: Setup NFS Clients
icon: dot-fill
---

The NFS server has been setup on the head node, now every other node must be set up as an NFS client.

First, a demonstration of the setup process on one node.



Begin by installing:
```bash
yum install -y -nfs-utils
```

Then open the file `/etc/fstab` and add:

```
chead1:/export/apps    /opt/apps     nfs    intr,rsize=32768,wsize=32768,vers=3,_netdev,nofail    0 0
chead1:/export/data    /opt/data     nfs    intr,rsize=32768,wsize=32768,vers=3,_netdev,nofail    0 0
chead1:/export/service /opt/service  nfs    intr,rsize=32768,wsize=32768,vers=3,_netdev,nofail    0 0
chead1:/export/site    /opt/site     nfs    intr,rsize=32768,wsize=32768,vers=3,_netdev,nofail    0 0
chead1:/home           /home         nfs    intr,rsize=32768,wsize=32768,vers=3,_netdev,nofail    0 0
```

Then save and exit.


Next, make some directories that will be used in future:
```bash
mkdir /opt/{apps,data,service,site}
```

Now the client is ready to start up:
```bash
systemctl start nfs
```
```bash
systemctl enable nfs
```

Lastly, mount NFS.
```bash
mount -a
```
```bash
df -h
```

At this point, this node is fully setup to be an NFS client. Repeat these steps on every other node (except the head node), and then NFS will be completely set up.


