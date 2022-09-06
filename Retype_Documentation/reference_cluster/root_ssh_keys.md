---
order: 90
label: SSH Keys for Root
icon: dot-fill
---

During setup and installation, the user will need to swap nodes. Adding ssh keys to root allows the user to ssh to all nodes without typing a password, thereby making installation easier.

First, become the root user:

```bash
sudo su -
```

Unless said otherwise, everything is done as the root user.

On the head node do:

```bash
ssh-keygen
```

If asked for a name or password, leave it blank so that it is the default.

This command creates a public and private key in the directory `~/.ssh` 

Copy the public key `id_rsa.pub` and go to one of your other nodes.

Become the root user, and go to the file `~/.ssh/authorized_keys`.

On a new line paste the public key. Now as root user we can log into this node without typing a password.

Copy and paste the public key into the authorised keys file of the root user of every node. Now root user can ssh into any node without typing a password.
