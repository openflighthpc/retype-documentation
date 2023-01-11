---
order: 70
label: 'd\. Configure SLURM'
icon: dot-fill
---





+++ Login node

On the login node:


1. Open the file `/opt/flight/opt/slurm/etc/slurm.conf` and add this information:
	```
	ControlMachine=chead1
	SlurmUser=nobody
	SlurmctldPort=6827
	SlurmdPort=6828
	AuthType=auth/munge
	StateSaveLocation=/opt/flight/opt/slurm/var/spool/slurm.state
	SlurmdSpoolDir=/opt/flight/opt/slurm/var/spool/slurmd.spool
	SwitchType=switch/none
	MpiDefault=none
	SlurmctldPidFile=/opt/flight/opt/slurm/var/run/slurmctld.pid
	ClusterName=mycluster1
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
	SlurmctldDebug=3
	SlurmctldLogFile=/opt/flight/opt/slurm/var/log/slurmctld.log
	SlurmdDebug=3
	SlurmdLogFile=/opt/flight/opt/slurm/var/log/slurmd.log
	JobCompType=jobcomp/none
	NodeName=cnode[01-02]
	PartitionName=all Nodes=ALL Default=YES MaxTime=UNLIMITED                         
	```

2. Create directories for SLURM.
	```bash
	mkdir -p /opt/flight/opt/slurm/var/{log,run,spool/slurm.state}
	```

3. Set the owner of the directories.
	```bash
	chown -R nobody: /opt/flight/opt/slurm/var/{log,run,spool}
	```

4. Generate a random 64 digit alphanumeric string to be used as a munge key.
	```bash
	tr -dc A-Za-z0-9 </dev/urandom | head -c 64 ; echo ''
	````

5. Copy the 64 digit code from the terminal, navigate to the file `/etc/munge/munge.key`, then paste it in.

6. Set the owner of the munge key.
	```
	chown munge: /etc/munge/munge.key
	```

7. Set permissions on the munge key.
	```bash
	chmod 400 /etc/munge/munge.key
	```

8. Start and enable munge and SLURM.
	```bash
	systemctl start munge
	systemctl enable munge
	systemctl start flight-slurmctld
	systemctl enable flight-slurmctld
	```

Now the SLURM server has been set up, the SLURM clients need to be set up on the other nodes.


+++ Compute Nodes

On a compute node:



1. Take the contents of the file `/opt/flight/opt/slurm/etc/slurm.conf` on the head node and copy it to the same location on the current node.

2. Create new directories for SLURM:
	```bash
	mkdir -p /opt/flight/opt/slurm/var/{log,run,spool}
	```

3. Set the owner of the new directories:
	```bash
	chown -R nobody: /opt/flight/opt/slurm/var/{log,run,spool}
	```

4. Take the munge key from the file `/etc/munge/munge.key` on the head node and make a munge key in the same location on the current node.

5. Set the owner of the munge key:
	```bash
	chown munge: /etc/munge/munge.key
	```
6. Set permissions on the munge key.
	```bash
	chmod 400 /etc/munge/munge.key
	```

7. Start munge and SLURM:
	```bash
	systemctl start munge
	systemctl enable munge
	systemctl start flight-slurmd
	systemctl enable flight-slurmd
	```

Repeat these steps on every other compute node.

+++

