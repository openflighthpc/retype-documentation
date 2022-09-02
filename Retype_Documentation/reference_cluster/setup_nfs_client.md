---
order: 60
label: Setup NFS Clients
icon: dot-fill
---

4 setup nfs client

node1:

yum install -y -nfs-utils

vim /etc/fstab

add:
chead1:/export/apps /opt/apps  nfs  intr,rsize=32768,wsize32768,vers=3,_netdev,nofail 0 0
again for

chead1:/export/apps /opt/apps  nfs  intr,rsize=32768,wsize32768,vers=3,_netdev,nofail 0 0
chead1:/export/service /opt/apps  nfs  intr,rsize=32768,wsize32768,vers=3,_netdev,nofail 0 0
chead1:/export/site /opt/apps  nfs  intr,rsize=32768,wsize32768,vers=3,_netdev,nofail 0 0
chead1:/home /home  nfs  intr,rsize=32768,wsize32768,vers=3,_netdev,nofail 0 0

save and exit

mkdir /opt/{apps,data,service,site}

systemctl start nfs

systemctl enable nfs

mount -a

df -h

now do this all on cnode02

