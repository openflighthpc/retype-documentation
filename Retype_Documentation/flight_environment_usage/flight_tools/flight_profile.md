---
order: 90
label: Flight Profile
icon: dot
data:
    access_host: 10.151.15.51
    compute_ip_range: 10.10.0.0/16
---


Flight profile is a tool that manages the profiles of cluster nodes. In this context, a profile is a cluster type, and the different types of nodes are identities. For example, a profile might be `slurm multinode`, and the identities would be `login` and `compute`. This page covers the sub-commands of `flight profile`, which are run in the format `flight profile <sub-command> --<option>`

### `configure`

When setting up a cluster's profile, this is the first command that needs to be run. When `flight profile configure` is run, the user will be guided through a series of questions that need to be answered to properly configure the cluster. There are too many questions to cover them all here, but the [cluster build methods](/cluster_build_methods/) section has more information about specific clusters. 

- `--reset-type` - After a cluster type has been chosen, it will be locked in when `configure` is run in the future. This argument allows the user to reset and select a different cluster type.

- `--show` - Shows the answers for the current configuration.

- `--answers` - Pass json text as the answers instead of using the menu. This could be done either by pasting text or passing the contents of a file (e.g. `flight profile configure --answers "$(cat /path/file.json)"` ).
    Here are some examples of what the json should be:
    +++ Slurm Standalone
    ```
    {
      "cluster_type": "openflight-slurm-standalone",
      "cluster_name": "my-cluster",
      "default_username": "flight",
      "default_password": "0penfl1ght",
      "access_host": "{{ access_host }}"
    }

    ```

    +++ Slurm Multinode
    ```
    {
      "cluster_type": "openflight-slurm-multinode",
      "cluster_name": "my-cluster",
      "nfs_server": "login1",
      "slurm_server": "login1",
      "default_username": "flight",
      "default_password": "0penfl1ght",
      "access_host": "{{ access_host }}",
      "compute_ip_range": "{{ compute_ip_range }}"
    }

    ```
    +++ Kubernetes Multinode
    ```
    {
      "cluster_type": "openflight-kubernetes-multinode",
      "cluster_name": "my-cluster",
      "default_username": "flight",
      "default_password": "0penfl1ght",
      "nfs_server": "login1",
      "access_host": "{{ access_host }}",
      "compute_ip_range": "{{ compute_ip_range }}",
      "pod_ip_range": "192.168.0.0/16"
    }
    ```

    +++ Jupyter
    ```
    {
      "cluster_type": "openflight-jupyter-standalone",
      "cluster_name": "my-cluster",
      "default_username": "flight",
      "default_password": "0penfl1ght",
      "access_host": "{{ access_host }}"
    }
    ```

    +++

    An example of using `answer` to configure a slurm multinode cluster would be:
    ```
    flight profile configure --answer '{  "cluster_type": "openflight-slurm-standalone",  "cluster_name": "my-cluster",  "default_username": "flight",  "default_password": "0penfl1ght",  "access_host": "{{ access_host }}"}'
    ```

- `--accept-defaults` - When using `--answers`, take the default values for any answers not given.

---

### `apply <node,node2...> <identity>`
Applies an identity to one or more nodes. e.g. `flight profile apply node01,node02` or `flight profile apply node01`
- `--force` - Overwrite the identity of a node that has already been applied to.
!!!
You can select multiple nodes at once by writing a comma separated list, or with square bracket expansion. E.g. `apply node[01-02] compute` would apply `compute` to `node01` and `node02`
!!!


---

### `avail`

Lists the available cluster types.

---

### `clean <node>`
Removes the data one or more nodes that failed application or removal from appearing in the list of profile accessible nodes. This means the node will show as `available`.

---

### `identities <type>`
Shows a list of all available identities for a cluster type. If there is no given cluster type, identities will be shown for the currently configured cluster type.

---

### `list`
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

### `prepare <type>`
Prepares a cluster type, completing dependencies. If no cluster type is specified then the currently configured one is used.
!!!
A cluster type must be prepared before it can be used.
!!!

---

### `remove <node,node...>`
Removes the identity of a node, so that it is no longer works as part of the cluster. 
- `--remove-hunter-entry` - Also remove it from the hunter list.
- `--force` - Bypass restrictions on using `remove` on a node.

!!!
`remove` is limited to only some identities, so not all identities can be removed.
!!!

!!!
You can select multiple nodes at once by writing a comma separated list, or with square bracket expansion. E.g. `remove node[01-02] compute` would apply `compute` to `node01` and `node02`
!!!

---

### `view <node>`

Shows the setup/removal progress of a node and its current status
- `--raw` - Shows the entire ansible log output.


---

## Auto-apply

Profile can automatically apply an identity to a node with the auto-apply configuration. This is done by configuring `flight hunter hunt` to automatically apply identities whenever a node is parsed with `auto-parse`.

!!!warning
You must have already configured flight profile with the `configure` command or else auto-applying will not work.
!!!

### Setup Auto-apply

1. Open the file `/opt/flight/opt/hunter/etc/config.yml`

!!!
You will need to have root user permissions to edit this config file.
!!!

2. Add these lines: ()
    ```
    auto_apply:
    <regex>: <identity>
    ```
    - You can add extra lines of `<regex>: <identity>` to catch more identities. e.g.
    ```
    auto_apply:
    cnode: compute
    chead: login
    ```
3. Restart the hunter service with `flight service restart hunter`.
    - Alternatively, you can stop the hunter service with `flight service stop hunter` and then run `flight hunter hunt`.

