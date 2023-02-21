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


## Testing

If all was successful, then the following should be the case on all nodes:

1. The flight user can be accessed by logging in:

    ```
    su - flight
    ```

2. After [starting flight](/flight_environment_usage/flight_overview/flight_system/) it is possible to ssh to any node from any node as the flight user.

3. The flight username and password can be used log in to the flight web-suite.