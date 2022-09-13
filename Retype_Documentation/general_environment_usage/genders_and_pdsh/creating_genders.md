---
order: 50
label: Creating genders
icon: dot
---

The process to create a gender is as follows:

First navigate to the genders file at `/opt/flight/etc/genders`, and open it with the editor of your choice

Next, add a gender in with the following format:

```
node01,node02,node03,node04,node05 gendername
```

There are alternate formats that make writing a gender easier:

```
node01,node02,node03,node04,node05:    node[01-05]
node3,node7,node9,node11:              node[3,7,9-11]
nodei,nodej,node0,node1,node2:         nodei,nodej,node[0-2]
```

For example:

```
node[01-05] genders
nodeA,nodeB,node[1,2,3,10-20],nodeC nodes
```

After adding the desired gender(s), save and close the file.


