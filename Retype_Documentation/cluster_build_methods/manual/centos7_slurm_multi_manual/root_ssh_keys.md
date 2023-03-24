---
order: 90
label: SSH Keys for Root
icon: dot
---

During setup and installation, the user will need to swap nodes. Adding ssh keys to root allows the user to ssh to all nodes without typing a password, thereby making installation easier. 

Follow the instructions on each of the tabs going from leftmost tab to rightmost tab.

+++ Head node
### On the head node
1. Become the root user:

    ```bash
    sudo su -
    ```

2. Generate an ssh keypair


    ```bash
    ssh-keygen
    ```

    !!!
    If asked for a name or password, leave it blank.
    !!!


3. Copy the public key found in `~/.ssh/id_rsa.pub` to your clipboard, it will be used on the compute nodes.


+++ Compute nodes
### On every compute node

1. Become the root user, 

    ```bash
    sudo su -
    ```

2. Open the file `~/.ssh/authorized_keys`

3. On a new line paste the public key, then save and exit.



Repeat these steps on every node other than the head node. Doing this allows us to log in as root user to any node without typing a password.

+++

!!!warning
Unless stated otherwise, everything is done as the root user.
!!!

Proceed to the next page after completing the instructions in each tab.


## Testing

If all was successful, then it should be possible to ssh from root on headnode into both of the compute nodes. E.g.

```
[root@chead1 ~]# ssh cnode01
Activate the web console with: systemctl enable --now cockpit.socket

Last login: Tue Sep 20 09:00:11 2022 from 10.50.0.13
[root@cnode01 ~]# logout
Connection to cnode01 closed.
[root@chead1 ~]# ssh cnode02
Activate the web console with: systemctl enable --now cockpit.socket

Last login: Tue Sep 20 09:00:18 2022 from 10.50.0.13
[root@cnode02 ~]# 
```