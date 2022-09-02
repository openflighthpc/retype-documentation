---
order: 0
label: Install Genders and PDSH
icon: dot-fill
---

A combination of genders and pdsh can allow for management and monitoring of multiple nodes at a time. 


Nodeattr and pdsh can be installed using the yum package manager, simply:

```bash
sudo yum -y install flight-pdsh
```

The priority of the OpenFlight pdsh command in the path can be configured with:

```bash
flight config set pdsh.priority X
```

Where `X` is one of:

- `system` - Prefer system PDSH
- `embedded` - Prefer OpenFlight PDSH
- `disabled` - Do not include OpenFlight PDSH in PATH


The process to create a gender is as follows:

First navigate to the genders file at `/opt/flight/etc/genders`, and open it

Next, add a gender in with the following format:

```
node01,node02,node03,node04,node05 gendername
```

After adding the desired gender(s), save and close the file.

