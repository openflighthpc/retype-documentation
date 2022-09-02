---
order: 70
label: Setup NFS Server
icon: dot-fill
---

3 - setup nfs

yum install nfs-utils



make a dir of all the things we want to share

mkdir /export

mkdir /export/{apps,data,service,site}
ensure permissions are okay

chmod 775 -R /export/

vim /etc/exports

/export/apps
/export/data 10.10.0.0/16(rw,no_root_squash,sync)
/export/service 10.10.0.0/16(rw,no_root_squash,sync)
/export/site
/home


bind mounts for nfs server

vim /etc/fstab


add:
/export/apps /opt/apps none defaults,bind 0 0
/export/data /opt/apps none defaults,bind 0 0
/export/service /opt/apps none defaults,bind 0 0
/export/site /opt/apps none defaults,bind 0 0

save and exit

mkdir /opt/{apps,data,service,site}


systemctl start nfs

systemctl enable nfs

exportfs -va

(v for verbose, a for all)

mount -a

NFS SERVER SETUP
