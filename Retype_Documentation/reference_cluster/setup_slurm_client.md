---
order: 20
label: Setup SLURM Clients
icon: dot-fill
---

The SLURM server was set up on the head node so now the SLURM clients need to be set up on the other nodes. Do **not** follow these instructions on the head node, only the other nodes.

1. Swap to a compute node

2. Install munge:
	```bash
	yum install -y munge munge-libs perl-Switch numactl
	```

3. Install the SLURM packages:
	```bash
	yum install -y flight-slurm flight-slurm-devel flight-slurm-perlapi flight-slurm-torque flight-slurm-slurmd flight-slurm-example-configs flight-slurm-libpmi
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
9. Lock the munge key so that it cannot be changed again:
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

Repeat these steps on every node (other than the head node).
