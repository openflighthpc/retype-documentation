---
order: 100
label: 'a\. Prepare Nodes'
icon: dot
---

This example instruction cluster consists of a login node and two compute nodes, but it is possible to use more.
Make sure to do all the instructions on a tab, then proceed the next tab and repeat.

1. Log into the login node

2. Become the root user and, unless otherwise stated, stay as the root user.


+++ Login node

3. Prepare the login node

a. Set the hostname.

    ```bash
    sudo hostnamectl set-hostname chead1.pri.mycluster1.cluster.local
    ```

b. Go to the file `/etc/hosts` and add this:

    ```bash
    10.50.0.13  chead1.pri.mycluster1.cluster.local chead1.pri chead1
    10.50.0.31  cnode01.pri.mycluster1.cluster.local cnode01.pri cnode01
    10.50.0.26  cnode02.pri.mycluster1.cluster.local cnode02.pri cnode02
    ```

    !!!
    The ip addresses will be different, make sure to change them.
    !!!

+++ Compute node 1

3. Prepare the first compute node

a. ssh into compute node 1 by using the hostname e.g. `ssh ip...name`

b. Set the hostname:

    ```bash
    sudo hostnamectl set-hostname cnode01.pri.mycluster1.cluster.local
    ```

c. Go to the file `/etc/hosts` and add this:

    ```bash
    10.50.0.13  chead1.pri.mycluster1.cluster.local chead1.pri chead1
    10.50.0.31  cnode01.pri.mycluster1.cluster.local cnode01.pri cnode01
    10.50.0.26  cnode02.pri.mycluster1.cluster.local cnode02.pri cnode02
    ```

    !!!
    The ip addresses will be different
    !!!

+++ Compute Node 2
3. Prepare the second compute node

a. ssh into compute node 2 by using the hostname e.g. `ssh ip...name`

b. Set the hostname:

    ```bash
    sudo hostnamectl set-hostname cnode02.pri.mycluster1.cluster.local
    ```

c. Go to the file `/etc/hosts` and add this:

    ```bash
    10.50.0.13  chead1.pri.mycluster1.cluster.local chead1.pri chead1
    10.50.0.31  cnode01.pri.mycluster1.cluster.local cnode01.pri cnode01
    10.50.0.26  cnode02.pri.mycluster1.cluster.local cnode02.pri cnode02
    ```

    !!!
    The ip addresses will be different
    !!!

+++

The node hostnames have been changed to `chead1`,`cnode01`, and `cnode02`. When SSHing into a node, be sure to use these hostnames.
