---
order: 95
label: Node Setup
icon: dot
---

Assuming that your nodes have already been created, and you have access to them, follow the instructions on each of the tabs going from leftmost tab to rightmost tab.

+++ chead1

### On the head node

1. If there is a firewall, disable it with:

	```bash
	sudo systemctl disable firewalld
	sudo systemctl stop firewalld
	```

2. If there is no firewall, run the mask command to prevent it from being set up in future:

    ```bash
    sudo systemctl mask firewalld
    ```

3. Disable SELINUX.

    ```bash
    sudo setenforce 0
    ```

4. Go to the file `/etc/selinux/config` and change the `SELINUX` value to `disabled`. This permanently disables SELINUX.
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

5. Set the hostname.

    ```bash
    sudo hostnamectl set-hostname chead1.pri.mycluster1.cluster.local
    ```

6. Go to the file `/etc/hosts` and add this:

    ```bash
    10.50.0.13  chead1.pri.mycluster1.cluster.local chead1.pri chead1
    10.50.0.31  cnode01.pri.mycluster1.cluster.local cnode01.pri cnode01
    10.50.0.26  cnode02.pri.mycluster1.cluster.local cnode02.pri cnode02
    ```

    !!!
    The ip addresses will be different
    !!!

+++ cnode01
### On the first compute node.

1. If there is a firewall, disable it with:

	```bash
	sudo systemctl disable firewalld
	sudo systemctl stop firewalld
	```

2. If there is no firewall, run the mask command to prevent it from being set up in future:

    ```bash
    sudo systemctl mask firewalld
    ```

3. Disable SELINUX.

    ```bash
    sudo setenforce 0
    ```

4. Go to the file `/etc/selinux/config` and change the `SELINUX` value to `disabled`. This permanently disables SELINUX.
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

5. Set the hostname:

    ```bash
    sudo hostnamectl set-hostname cnode01.pri.mycluster1.cluster.local
    ```

6. Go to the file `/etc/hosts` and add this:

    ```bash
    10.50.0.13  chead1.pri.mycluster1.cluster.local chead1.pri chead1
    10.50.0.31  cnode01.pri.mycluster1.cluster.local cnode01.pri cnode01
    10.50.0.26  cnode02.pri.mycluster1.cluster.local cnode02.pri cnode02
    ```

    !!!
    The ip addresses will be different
    !!!

+++cnode02
### On the second compute node.

1. If there is a firewall, disable it with:

	```bash
	sudo systemctl disable firewalld
	sudo systemctl stop firewalld
	```

2. If there is no firewall, run the mask command to prevent it from being set up in future:

    ```bash
    sudo systemctl mask firewalld
    ```

3. Disable SELINUX.

    ```bash
    sudo setenforce 0
    ```

4. Go to the file `/etc/selinux/config` and change the `SELINUX` value to `disabled`. This permanently disables SELINUX.
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

5. Set the hostname:

    ```bash
    sudo hostnamectl set-hostname cnode02.pri.mycluster1.cluster.local
    ```

6. Go to the file `/etc/hosts` and add this:

    ```bash
    10.50.0.13  chead1.pri.mycluster1.cluster.local chead1.pri chead1
    10.50.0.31  cnode01.pri.mycluster1.cluster.local cnode01.pri cnode01
    10.50.0.26  cnode02.pri.mycluster1.cluster.local cnode02.pri cnode02
    ```

    !!!
    The ip addresses will be different
    !!!

+++

Proceed to the next page after completing the instructions in each tab.


