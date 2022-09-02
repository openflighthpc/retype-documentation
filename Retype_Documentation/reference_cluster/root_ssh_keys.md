---
order: 90
label: 
icon: 
---

1
adding root ssh keys
a way to passwordlessly move around

from head node: 
ssh-keygen


that creates a public and private key in the .ssh directory


take the public key and copy it to both our compute nodes in the authorised keys directory for root user

now as root user we can log into other nodes with no password
