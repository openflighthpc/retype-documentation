---
order: 50
label: Install Flight
icon: dot
---


Install flight on a node.

1. Install the OpenFlight release RPM:
    ```bash
    dnf install -y https://repo.openflighthpc.org/openflight/centos/8/x86_64/openflighthpc-release-3-1.noarch.rpm
    ```

2. Add the Power Tools repository:
    ```bash
    dnf config-manager --set-enabled powertools
    ```

3. Rebuild the yum cache:
    ```bash
    dnf makecache
    ```




3. Install the flight packages:
	```bash
	dnf install -y flight-user-suite flight-plugin-system-systemd-service
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
