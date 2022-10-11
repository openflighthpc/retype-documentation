---
order: 50
label: Install Flight
icon: dot
---


On **every** node:



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

5. Log out and log back in for the environment to load.

6. Start flight, and enable it on start up:
	```bash
	flight start
	flight set always on
	```

7. Change the name of the cluster:
	```bash
	flight config set cluster.name mycluster1
	```
8. Log out and log back in for the environment to reload.

Flight has been installed on this node. Follow the instructions on each node until they all have Flight.

## Testing

If all was successful, then the following should be the case on all nodes:

1. The command `yum repolist` should display the openflight package. E.g. on head node:

	```
    [root@chead1 ~]# yum repolist
    Loaded plugins: fastestmirror
    Loading mirror speeds from cached hostfile
     * base: mirror.freethought-internet.co.uk
     * epel: epel.mirror.wearetriple.com
     * extras: repo.uk.bigstepcloud.com
     * updates: mirror.mhd.uk.as44574.net
    repo id             repo name                            status
    base/7/x86_64       CentOS-7 - Base                      10,072
    epel/x86_64         Extra Packages for Enterprise Linux  13,750
    extras/7/x86_64     CentOS-7 - Extras                       516
    openflight/7/x86_64 OpenFlight - Base                        81
    updates/7/x86_64    CentOS-7 - Updates                    4,160
    repolist: 28,579
	```

2. The command `systemctl status flight-service` shows the service as active with no errors.

3. The flight environment should be started (`flight start`).

3. The command prompt should display the cluster name. E.g.

    ```
    [root@chead1 (mycluster1) ~]# 
    ```