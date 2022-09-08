---
order: 90
label: SSH Keys for Root
icon: dot-fill
---

During setup and installation, the user will need to swap nodes. Adding ssh keys to root allows the user to ssh to all nodes without typing a password, thereby making installation easier.




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


3. Copy the public key found in `~/.ssh/id_rsa.pub`.



### Every other node

1. Become the root user, 

    ```bash
    sudo su -
    ```

2. Open the file `~/.ssh/authorized_keys`

3. On a new line paste the public key, then save and exit.



Repeat the "Every other node" steps on every node other than the head node. Doing this allows us to log in as root user to any node without typing a password.


!!!warning
Unless stated otherwise, everything is done as the root user.
!!!