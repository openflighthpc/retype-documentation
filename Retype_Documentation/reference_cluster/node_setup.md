---
order: 95
label: Node Setup
icon: dot-fill
---


Assuming that your nodes have already been created, and you have access to them:

### On the head node

Launch the head node, and set the hostname:

```bash
sudo hostnamectl set-hostname chead1.pri.mycluster1.cluster.local
```

Go to the file `/etc/hosts` and add this:

```bash
10.50.0.23  cnode01.pri.mycluster1.cluster.local cnode01.pri cnode01
10.50.0.46  cnode02.pri.mycluster1.cluster.local cnode02.pri cnode02
```
!!!
The ip address may be slightly different.
!!!

### On the first compute node.

Set the hostname:

```bash
sudo hostnamectl set-hostname cnode01.pri.mycluster1.cluster.local
```

Go to the file `/etc/hosts` and add this:

```bash
10.50.0.50  chead1.pri.mycluster1.cluster.local chead1.pri chead1
10.50.0.46  cnode02.pri.mycluster1.cluster.local cnode02.pri cnode02
```

### On the second compute node.

Set the hostname:

```bash
sudo hostnamectl set-hostname cnode01.pri.mycluster1.cluster.local
```

Go to the file `/etc/hosts` and add this:

```bash
10.50.0.50  chead1.pri.mycluster1.cluster.local chead1.pri chead1
10.50.0.23  cnode01.pri.mycluster1.cluster.local cnode01.pri cnode01
```
