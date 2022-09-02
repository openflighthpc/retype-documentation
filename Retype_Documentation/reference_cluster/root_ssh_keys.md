---
order: 90
label: 
icon: 
---

During setup and installation, the user will need to swap nodes. Adding ssh keys to root allows the user to ssh to all nodes without typing a password, thereby making installation easier.

First, become the root user:

```bash
sudo su -
```

On the head node do:

```bash
ssh-keygen
```

This command creates a public and private key in the directory `~/.ssh` 

Copy the public key and go to one of your other nodes:

```bash
ssh cnode01
```

!!!
Your other node may be named something else.
!!!

Go to the authorised key file:

```bash
vim ~/.ssh/authorized_keys
```

On a new line paste the public key. Now as root user we can log into this node without typing a password.

Copy and paste the public key into the authorised keys file of every node. Now root user can ssh into any node without typing a password.
