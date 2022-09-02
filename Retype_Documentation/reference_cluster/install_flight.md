---
order: 50
label: Install Flight
icon: dot-fill
---

step 5 install flight

on head node:

install flight


then
yum install -y flight-user-suite flight-plugin-systemd-service

systemctl start flight-service
systemctl enable flight-service

log out of root

log back in

flight start

flight set always on

flight config set cluster.name mycluster1



now do it on all other nodes
