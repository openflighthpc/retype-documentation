---
order: 30
label: Setup SLURM Server
icon: dot-fill
---

The following section has to be done on the **head** node. 

1. Swap to the head node (unless already on it).

2. Install munge.
	```bash
	yum install -y munge munge-libs perl-Switch numactl
	```

3. Install the SLURM packages.
	```bash
	yum install -y flight-slurm flight-slurm-slurmctld flight-slurm-devel flight-slurm-perlapi flight-slurm-torque flight-slurm-slurmd flight-slurm-example-configs flight-slurm-libpmi
	```

4. Open the file `/opt/flight/opt/slurm/etc/slurm.conf` and add this information:
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

10. Lock the munge key so that it cannot be changed again.
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

Now the SLURM server has been set up, the SLURM clients need to be set up on the other nodes.