---
order: 20
label: Setup SLURM Clients
icon: dot
---

The SLURM server was set up on the head node so now the SLURM clients need to be set up on the compute nodes. Do **not** follow these instructions on the head node, only the compute nodes.

1. Swap to a compute node

2. Install munge:

	```bash
	dnf install -y munge munge-libs perl-Switch numactl
	```

3. Install the SLURM packages:
	```bash
	dnf install -y flight-slurm flight-slurm-devel flight-slurm-perlapi flight-slurm-torque flight-slurm-slurmd flight-slurm-example-configs flight-slurm-libpmi
	```

4. Take the contents of the file `/opt/flight/opt/slurm/etc/slurm.conf` on the head node and copy it to the same location on the current node.

5. Create new directories for SLURM:
	```bash
	mkdir -p /opt/flight/opt/slurm/var/{log,run,spool}
	```

6. Set the owner of the new directories:
	```bash
	chown -R nobody: /opt/flight/opt/slurm/var/{log,run,spool}
	```

7. Take the munge key from the file `/etc/munge/munge.key` on the head node and make a munge key in the same location on the current node.

8. Set the owner of the munge key:
	```bash
	chown munge: /etc/munge/munge.key
	```
9. Set permissions on the munge key.
	```bash
	chmod 400 /etc/munge/munge.key
	```

10. Start munge and SLURM:
	```bash
	systemctl start munge
	systemctl enable munge
	systemctl start flight-slurmd
	systemctl enable flight-slurmd
	```

Repeat these steps on every other compute node.


## Testing

If all was successful, then the following should be the case on the compute nodes:

1. The command `systemctl status munge` shows the service as active with no errors.

2. The command `systemctl status flight-slurmd` shows the service as active with no errors.

3. The file `/opt/flight/opt/slurm/etc/slurm.conf` has all the necessary options set. An example file is given in the instructions for SLURM server setup.

4. The `/opt/flight/opt/slurm/var` directory exists, and contains these three directories:

	```
	[root@chead1 (mycluster1) ~]# ls /opt/flight/opt/slurm/var/
	log  run  spool
	```

5. The `/opt/flight/opt/slurm/var` directory has these permissions:

	```
	[root@cnode01 (mycluster1) ~]# ls -l /opt/flight/opt/slurm/var/
	total 0
	drwxr-xr-x. 2 nobody nobody 6 Sep 20 14:54 log
	drwxr-xr-x. 2 nobody nobody 6 Sep 20 14:54 run
	drwxr-xr-x. 2 nobody nobody 6 Sep 20 14:54 spool
	```


6. The munge key (`/etc/munge/munge.key`) should be the same on all nodes.

7. The munge key (`/etc/munge/munge.key`) should have these permissions:

	```
	[root@cnode01 (mycluster1) ~]# ls -l /etc/munge/munge.key
	-r--------. 1 munge munge 65 Sep 20 14:56 /etc/munge/munge.key
	```