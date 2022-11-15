---
order: 80
label: Manually Configuring a SLURM Standalone Cluster
icon: dot-fill
---

Once all the node needed for a cluster have been created, they need to be configured. This page covers how to manually configure a standalone cluster, but OpenflightHPC recommends using [Flight Profile](/flight_profile/solo_standalone_config/) for setup, as it does everything automatically.
In the case of a standalone cluster, you will only need 1 node, if you haven't already, create it by following the [Login Node](/flight_solo/aws/setup_with_marketplace_login/) instructions.

Flight Solo comes with the Flight user suite installed but not configured. There are no other nodes to connect to so setup is simple.


1. add domain

```
flight web-suite set-domain 3.8.154.86
```

2. restart flight web-suite
```
flight web-suite restart
```

3. setup slurm?
```
/opt/flight/opt/slurm/etc/slurm.conf
```
```
ClusterName=mycluster1
ControlMachine=localhost
SlurmUser=nobody
SlurmctldPort=6827
SlurmdPort=6828
AuthType=auth/munge
StateSaveLocation=/opt/flight/opt/slurm/var/spool/slurm.state
SlurmdSpoolDir=/opt/flight/opt/slurm/var/spool/slurmd.spool
SwitchType=switch/none
MpiDefault=none
SlurmctldPidFile=/opt/flight/opt/slurm/var/run/slurmctld.pid
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
NodeName=localhost 
PartitionName=all Nodes=ALL Default=YES MaxTime=UNLIMITED

```

```
sudo echo "172.31.28.114 standalone1.pri.mycluster1.cluster.local standalone1.pri standalone" >> /etc/hosts
```

```
mkdir -p /opt/flight/opt/slurm/var/{log,run,spool/slurm.state}
```
```
chown -R nobody: /opt/flight/opt/slurm/var/{log,run,spool}
```

4. munge


5. Create directories for SLURM.
	```bash
	mkdir -p /opt/flight/opt/slurm/var/{log,run,spool/slurm.state}
	```

6. Set the owner of the directories.
	```bash
	chown -R nobody: /opt/flight/opt/slurm/var/{log,run,spool}
	```

7. Generate a random 64 digit alphanumeric string to be used as a munge key.
	```bash
	tr -dc A-Za-z0-9 </dev/urandom | head -c 64 ; echo ''
	````

8. Copy the 64 digit code from the terminal, navigate to the file `/etc/munge/munge.key`, then paste it in.

9. Set the owner of the munge key.
	```
	chown munge: /etc/munge/munge.key
	```

10. Set permissions on the munge key.
	```bash
	chmod 400 /etc/munge/munge.key
	```

    11. Start and enable munge and SLURM.
	```bash
	systemctl start munge
	systemctl enable munge
	systemctl start flight-slurmctld
	systemctl enable flight-slurmctld
	```

4. set cluster name?

```
flight config set cluster.name mycluster1
```

5. 
