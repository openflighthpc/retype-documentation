---
order: 50
label: Install Flight
icon: dot-fill
---

On the head node install Flight.



Add the flight package:
```bash
sudo yum install -y https://repo.openflighthpc.org/pub/centos/7/openflighthpc-release-latest.noarch.rpm
```

Rebuild the yum cache:
```bash
sudo yum makecache
```
Then install the flight packages:
```bash
sudo yum install -y flight-user-suite flight-plugin-systemd-service
```

Now start and enable flight:

```bash
systemctl start flight-service
```
```bash
systemctl enable flight-service
```

Flight has now been installed, but for it to appear, the user needs to log out of root, and then log back in.


Flight should now have shown the startup message.

Start flight with:
```bash
flight start
```

It is recommended to set flight to be always on:
```bash
flight set always on
```

You may also change the name of the cluster:
```bash
flight config set cluster.name mycluster1
```


Flight has been installed on the head node. Follow the instructions on each node until they all have Flight.
