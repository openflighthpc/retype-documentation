---
order: 30
label: Setup SLURM Server
icon: dot-fill
---

step 7 SLURM

yum install -y munge munge-libs perl-Switch numactl


yum install -y install flight-slurm flight-slurm-slurmctld flight-slurm-devel flight-slurm-perlapi flight-slurm-torque flight-slurm-slurmd flight-slurm-example-configs flight-slurm-libpmi

vim /opt/flight/opt/slurm/etc/slurm.conf

set Nodename

example of slurm conf file

mkdir -p /opt/flight/opt/slurm/var/{log,run,spool/slurm.stare}
chown -R nobody: /opt/flight/opt/slurm/var/{log,run,spool}

tr -dc A-Za-z0-9 </dev/urandam | head -c 64 ; eco ‘’

put random numbers in munge file

vim /etc/munge/munge.key

set owner:

chown munge: /etc/munge/munge.key

lock perms to no read
chmod 400 /etc/munge/munge.key

systemctl start munge
systemctl enable munge

systemctl start flight-slurmctld


sinfo -Nl 
shows slurm running

INSTALLED A SLURM SERVER
