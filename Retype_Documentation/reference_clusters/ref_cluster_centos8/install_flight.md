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

3. Rebuild the dnf cache:
    ```bash
    dnf makecache
    ```

4. Install the flight packages:
	```bash
	dnf install -y flight-user-suite flight-plugin-system-systemd-service
	```

5. Start and enable flight:
	```bash
	systemctl start flight-service
	systemctl enable flight-service
	```

6. Log out and log back in for the environment to load.

7. Start flight, and enable it on start up:
	```bash
	flight start
	flight set always on
	```

8. Change the name of the cluster:
	```bash
	flight config set cluster.name mycluster1
	```

9. Log out and log back in for the environment to reload.


Flight has been installed on this node. Follow the instructions on each node until they all have Flight.

## Testing

If all was successful, then the following should be the case on all nodes:

1. The command `dnf repolist` should display the openflight and powertools packages. E.g. on head node:

	```
	[root@chead1 ~]# dnf repolist
	repo id            repo name
	appstream          CentOS Stream 8 - AppStream
	baseos             CentOS Stream 8 - BaseOS
	epel               Extra Packages for Enterprise Linux 8 - x86_64
	epel-modular       Extra Packages for Enterprise Linux Modular 8 - x86_64
	extras             CentOS Stream 8 - Extras
	openflight         OpenFlight - Base
	powertools         CentOS Stream 8 - PowerTools
	```

2. The command `systemctl status flight-service` shows the service as active with no errors.

3. The flight environment should be started (`flight start`).

3. The command prompt should display the cluster name. E.g.

    ```
    [root@chead1 (mycluster1) ~]# 
    ```