---
order: 60
label: 'e\. Create Shared User'
icon: dot-fill
---


We will create a shared user by making the exact same user on every node.

+++ Head node
### On the head node

1. Add a user named `flight2`
	```bash
	useradd -d /home/flight2 -u 1234 flight2 
	```

2. Set the new user's password.
	```bash
	passwd flight2
	```

+++ Compute nodes
### On the compute nodes

1. Add a user named `flight2`
	```bash
	useradd -d /home/flight2 -u 1234 flight2 -M
	```
	!!!
	The `-M` command is important because it creates a user with no home directory. The home directory for this user is created on the head node, and shared by NFS.
	!!!

2. Set the new user's password, and make it the same as on the head node.
	```bash
	passwd flight2
	```

Repeat these steps on all compute nodes.
+++
