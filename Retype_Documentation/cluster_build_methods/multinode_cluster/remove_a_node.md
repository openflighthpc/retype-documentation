---
order: 20
label: '6\. Removing a node from an existing cluster'
icon: dot
---

Sometimes, it may be necessary to remove a node from a cluster. This can be done with the following steps:

1. Run the command `flight profile remove <nodename>`
e.g.
```
[flight@chead1 ~]$ flight profile remove node01
Removing host 'node01'
The removal process has begun. Refer to `flight profile list` or `flight profile view` for more details
[flight@chead1 ~]$ 
```

2. Wait for the process to finish. On a successful removal, `flight profile list` will display the node as `available`. e.g.
```
[flight@chead1 ~]$ flight profile list
┌────────┬──────────┬───────────┐
│ Node   │ Identity │ Status    │
├────────┼──────────┼───────────┤
│ node02 │ compute  │ complete  │
│ node01 │          │ available │
│ login1 │ login    │ complete  │
└────────┴──────────┴───────────┘

```


There are additional options to help with the removal of nodes. 
- `--remove-hunter-entry` also removes the node's hunter entry (if there is one).
- `--force` bypasses restrictions on removing a node, such as if the removal initially fails and needs to be retried.


!!!
If a node has been removed from profile and hunter, it may be worth deleting the instance it runs on.
!!!