---
order: 20
label: 
icon: 
---

step 8 SLURM CLIENT

on node 1
yum install -y munge munge-libs perl-Switch numactl

yum install -y flight-slurm flight-slurm-devel flight-slurm-perlapi flight-slurm-torque flight-slurm-slurmd flight-slurm-example-configs flight-slurm-libpmi


what is in slurm.conf in the server needs to be on the clients


mkdir -p /opt/flight/opt/slurm/var/{log,run,spool}

chown -R nobody: /opt/flight/opt/slurm/var/{log,run,spool}

make the munge.key from the head node into the other nodes

make sure the munge user owns it

and locked in persm

start and enable munge with systemctl

systemctl start flight-slurmd

systemctl enable flight-slurmd




now do it on all other nodes
