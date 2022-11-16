---
order: 80
label: '2\. Manually Configuring a SLURM Standalone Cluster'
icon: dot-fill
---

Once all the node needed for a cluster have been created, they need to be configured. This page covers how to manually configure a standalone cluster, but OpenflightHPC recommends using the automatic configuration outlined in the [AWS section](/cluster_build_methods/aws/solo_slurm_single_profile/solo_standalone_profile_config/).
In the case of a standalone cluster, you will only need 1 node, if you haven't already, create it by following the instructions on the previous page

Flight Solo comes with the Flight user suite installed but not configured. There are no other nodes to connect to so setup is simple.


1. Set the hostname.

    ```bash
    sudo hostnamectl set-hostname standalone1.pri.mycluster1.cluster.local
    ```

2. Go to the file `/etc/hosts` and add this: (make sure to add the local IP)

    ```
    <local-IP> standalone1.pri.mycluster1.cluster.local standalone1.pri chead1
    ```

3. Change the name of the cluster:
	```bash
	flight config set cluster.name mycluster1
	```

4. Set the domain name to the hostname or ip address that Web-Suite will be accessed through. This also creates a self-certified certificate.
    ```bash
    flight web-suite set-domain <name/IP>
    ```

5. Restart web suite to apply changes:
    ```bash
    flight web-suite restart
    ```


6. Open the file `/opt/flight/opt/slurm/etc/slurm.conf` and add this information:
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
	SlurmctldDebug=3
	SlurmctldLogFile=/opt/flight/opt/slurm/var/log/slurm/slurmctld.log
	SlurmdDebug=3
	SlurmdLogFile=/opt/flight/opt/slurm/var/log/slurm/slurmd.log
	JobCompType=jobcomp/none
	NodeName=localhost 
	PartitionName=all Nodes=ALL Default=YES MaxTime=UNLIMITED
	```

7. Create directories for SLURM.
	```bash
	mkdir -p /opt/flight/opt/slurm/var/{log,run,spool/slurm.state}
	```

```
mkdir /opt/flight/opt/slurm/var/log/slurm/
```
 

8. Set the owner of the directories.
	```bash
	chown -R nobody: /opt/flight/opt/slurm/var/{log,run,spool}
	```

9. Generate a random 64 digit alphanumeric string to be used as a munge key.
	```bash
	tr -dc A-Za-z0-9 </dev/urandom | head -c 64 ; echo ''
	````

10. Copy the 64 digit code from the terminal, navigate to the file `/etc/munge/munge.key`, then paste it in.

11. Set the owner of the munge key.
	```
	chown munge: /etc/munge/munge.key
	```

12. Set permissions on the munge key.
	```bash
	chmod 400 /etc/munge/munge.key
	```

13. Start and enable munge and SLURM.
	```bash
	systemctl start munge
	systemctl enable munge
	systemctl start flight-slurmctld
	systemctl enable flight-slurmctld
    systemctl start flight-slurmd
    systemctl enable flight-slurmd
	```