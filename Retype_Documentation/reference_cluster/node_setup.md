---
order: 95
label: Node Setup
icon: dot-fill
---

Assuming that your nodes have already been created, and you have access to them:



### On the head node

1. If there is a firewall, disable it with:

```bash
sudo systemctl disable firewalld
sudo systemctl stop firewalld
```

2. Go to the file `/etc/selinux/config` and change the `SELINUX` value to `disabled`.
```bash
# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#     enforcing - SELinux security policy is enforced.
#     permissive - SELinux prints warnings instead of enforcing.
#     disabled - No SELinux policy is loaded.
SELINUX=disabled
# SELINUXTYPE= can take one of three values:
#     targeted - Targeted processes are protected,
#     minimum - Modification of targeted policy. Only selected processes are protected.
#     mls - Multi Level Security protection.
SELINUXTYPE=targeted

```

3. Launch the head node, and set the hostname:

```bash
sudo hostnamectl set-hostname chead1.pri.mycluster1.cluster.local
```

4. Go to the file `/etc/hosts` and add this:

```bash
10.50.0.21  cnode01.pri.mycluster1.cluster.local cnode01.pri cnode01
10.50.0.22  cnode02.pri.mycluster1.cluster.local cnode02.pri cnode02
10.50.0.36  chead1.pri.mycluster1.cluster.local chead1.pri chead1
```
!!!
The ip address may be slightly different.
!!!


### On the first compute node.

1. Change to your designated first compute node.

2. If there is a firewall, disable it with:

```bash
sudo systemctl disable firewalld
sudo systemctl stop firewalld
```

3. Go to the file `/etc/selinux/config` and change the `SELINUX` value to `disabled`.


4. Set the hostname:

```bash
sudo hostnamectl set-hostname cnode01.pri.mycluster1.cluster.local
```

5. Go to the file `/etc/hosts` and add this:

```bash
10.50.0.21  cnode01.pri.mycluster1.cluster.local cnode01.pri cnode01
10.50.0.22  cnode02.pri.mycluster1.cluster.local cnode02.pri cnode02
10.50.0.36  chead1.pri.mycluster1.cluster.local chead1.pri chead1
```

### On the second compute node.

1. Change to your designated first compute node.

2. If there is a firewall, disable it with:

```bash
sudo systemctl disable firewalld
sudo systemctl stop firewalld
```

3. Go to the file `/etc/selinux/config` and change the `SELINUX` value to `disabled`.

4. Set the hostname:

```bash
sudo hostnamectl set-hostname cnode02.pri.mycluster1.cluster.local
```

5. Go to the file `/etc/hosts` and add this:

```bash
10.50.0.21  cnode01.pri.mycluster1.cluster.local cnode01.pri cnode01
10.50.0.22  cnode02.pri.mycluster1.cluster.local cnode02.pri cnode02
10.50.0.36  chead1.pri.mycluster1.cluster.local chead1.pri chead1
```


!!!
The instructions for each type of node are similar but not the same.
!!!