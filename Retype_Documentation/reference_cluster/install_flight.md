---
order: 50
label: Install Flight
icon: dot-fill
---


Install flight on a node.



1. Add the flight package:
	```bash
	sudo yum install -y https://repo.openflighthpc.org/pub/centos/7/openflighthpc-release-latest.noarch.rpm
	```

2. Rebuild the yum cache:
	```bash
	sudo yum makecache
	```

3. Install the flight packages:
	```bash
	sudo yum install -y flight-user-suite flight-plugin-systemd-service
	```

4. Start and enable flight:
	```bash
	systemctl start flight-service
	systemctl enable flight-service
	```

5. Log out of and then back into the current node.

6. Start flight, and enable it on start up:
	```bash
	flight start
	flight set always on
	```

7. Change the name of the cluster:
	```bash
	flight config set cluster.name mycluster1
	```


Flight has been installed on this node. Follow the instructions on each node until they all have Flight.
