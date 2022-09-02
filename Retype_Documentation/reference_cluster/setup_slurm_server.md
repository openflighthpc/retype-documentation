---
order: 30
label: Setup SLURM Server
icon: dot-fill
---

The following section has to be done on the head node, so swap to the head node (unless already on it).

Install munge:
```bash
yum install -y munge munge-libs perl-Switch numactl
```

Install the SLURM packages:
```bash
yum install -y install flight-slurm flight-slurm-slurmctld flight-slurm-devel flight-slurm-perlapi flight-slurm-torque flight-slurm-slurmd flight-slurm-example-configs flight-slurm-libpmi
```

Go to the file `/opt/flight/opt/slurm/etc/slurm.conf` and set Nodename to the nodes available, it will look something like this:

```
SlurmdPidFile=/opt/flight/opt/slurm/var/run/slurmd.pid
ProctrackType=proctrack/pgid
ReturnToService=2
SlurmctldTimeout=300
SlurmdTimeout=300
InactiveLimit=0
MinJobAge=300
KillWait=30
Waittime=0
SchedulerType=sched/backfill
SelectType=select/cons_res
SelectTypeParameters=CR_CORE_Memory
FastSchedule=1
SlurmctldDebug=3
SlurmctldLogFile=/opt/flight/opt/slurm/var/log/slurm/slurmctld.log
SlurmdDebug=3
SlurmdLogFile=/opt/flight/opt/slurm/var/log/slurm/slurmd.log
JobCompType=jobcomp/none
NodeName=cnode[01-02]
PartitionName=all Nodes=ALL Default=YES MaxTime=UNLIMITED
"/opt/flight/opt/slurm/etc/slurm.conf" 31L, 904C   
```

On this cluster the nodes are `cnode01` and `cnode02`, but that can be shorted to `cnode[01-02]`.

Next several directories need to be created for SLURM to function:
```bash
mkdir -p /opt/flight/opt/slurm/var/{log,run,spool/slurm.stare}
```

Set the owner of the directories:
```bash
chown -R nobody: /opt/flight/opt/slurm/var/{log,run,spool}
```

Generate a random 64 digit alphanumeric string to be used as a munge key.
```bash
tr -dc A-Za-z0-9 </dev/urandam | head -c 64 ; eco ‘’
````

Copy the code and navigate to the file `/etc/munge/munge.key`, then paste the key in.




Set the owner of the munge key:
```
chown munge: /etc/munge/munge.key
```

Then lock the munge key so that it cannot be changed again:
```bash
chmod 400 /etc/munge/munge.key
```

Finally start everything to begin SLURM:
```bash
systemctl start munge
```
```bash
systemctl enable munge
```
```bash
systemctl start flight-slurmctld
```
```bash
systemctl enable flight-slurmctld
```

Now the SLURM server has been set up, the SLURM clients need to be set up on the other nodes.