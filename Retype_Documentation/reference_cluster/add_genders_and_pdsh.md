---
order: 0
label: Install Genders and PDSH
icon: dot-fill
---

A combination of genders and pdsh can allow for management and monitoring of multiple nodes at a time. 


This only needs to be done on the head node.

```bash
sudo yum -y install flight-pdsh
```

Next create a gender for all the nodes.

Navigate to the genders file at `/opt/flight/etc/genders`, and open it

Add a gender in the following format:

```
cnode01,cnode02 nodes
```

Save and close the file.

