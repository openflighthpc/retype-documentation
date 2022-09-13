---
order: 10
label: Create Shared User
icon: dot
---

We will create a shared user by making the exact same user on every node, follow the instructions on the tabs from left to right.


+++ Head node
### On the head node

1. Add a user named `flight`
	```bash
	useradd -d /home/flight -u 1234 flight 
	```

2. Set the new user's password.
	```bash
	passwd flight
	```

+++ Compute nodes
### On the compute nodes

1. Add a user named `flight`
	```bash
	useradd -d /home/flight -u 1234 flight -M
	```
	!!!
	The `-M` command is important because it creates a user with no home directory. The home directory for this user is created on the head node, and shared by NFS.
	!!!

2. Set the new user's password, and make it the same as on the head node.
	```bash
	passwd flight
	```

Repeat these steps on all compute nodes.
+++