---
order: 0
label: Install Genders and PDSH
icon: dot
---

A combination of genders and pdsh can allow for management and monitoring of multiple nodes at a time. 


This **only** needs to be done on the **head** node.

1. Swap to the head node (unless already on it).

2. Install flight-pdsh.
	```bash
	sudo yum -y install flight-pdsh
	```

3. Navigate to the genders file at `/opt/flight/etc/genders`, and open it.

4. Add a gender in the following format to the genders file. Then save and close the file.
	```
	cnode01,cnode02 nodes
	```
5. Log out and log back in for the environment to load.

## Testing

If all was successful, then the following should be the case on the head node:

1. The following commands should run without errors:
    ```
    nodeattr -s nodes
    ```
    ```
    pdsh -g nodes uptime
    ```

2. The file `/opt/flight/etc/genders` should contain genders for use with the installed commands.