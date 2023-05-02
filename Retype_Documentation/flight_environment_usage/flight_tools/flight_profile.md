---
order: 90
label: Flight Profile
icon: dot
---

Flight profile is a tool that manages the profiles of cluster nodes. In this context, a profile is a cluster type, and the different types of nodes are identities. For example, a profile might be `slurm multinode`, and the identities would be `login` and `compute`.

#### `configure`

When setting up a cluster's profile, this is the first command that needs to be run. When `flight profile configure` is run, the user will be guided through a series of questions that need to be answered to properly configure the cluster. There are too many questions to cover them all here, but the [cluster build methods](/cluster_build_methods/) section has more information about specific clusters.

- `--show` - Shows the answers for the current configuration.

---

#### `apply <node,node2...> <identity>`
Applies an identity to one or more nodes. e.g. `flight profile apply node01,node02` or `flight profile apply node01`
- `--force` - Overwrite the identity of a node that has already been applied to.


---

#### `avail`

Lists the available cluster types.

---

#### `clean <node>`
Removes the data one or more nodes that failed application or removal from appearing in the list of profile accessible nodes. This means the node will show as `available`.

---

#### `identities <type>`
Shows a list of all available identities for a cluster type. If there is no given cluster type, identities will be shown for the currently configured cluster type.

---

#### `list`
Displays the identity and status of every node available to profile. e.g.
```
[flight@chead1 (mycluster1) [login1] ~]$ flight profile list
┌────────┬──────────┬───────────┐
│ Node   │ Identity │ Status    │
├────────┼──────────┼───────────┤
│ login1 │ login    │ complete  │
│ node02 │ compute  │ failed    │
│ node01 │          │ available │
└────────┴──────────┴───────────┘
```

---

#### `prepare <type>`
Prepares a cluster type, completing dependencies. If no cluster type is specified then the currently configured one is used.
!!!
A cluster type must be prepared before it can be used.
!!!

---

#### `remove <node,node...>`
Removes the identity of a node, so that it is no longer works as part of the cluster. 
- `--remove-hunter-entry` - Also remove it from the hunter list.
- `--force` - Bypass restrictions on using `remove` on a node.

!!!
`remove` is limited to only some identities, so not all identities can be removed.
!!!

---

#### `view <node>`

Shows the setup/removal progress of a node and its current status
- `--raw` - Shows the entire ansible log output.



