---
order: 50
label: Finding the names of your compute nodes
icon: dot
---

The hostnames of compute nodes usually follow a sequential order (e.g. node01, node02, node03… node10). OpenFlight Compute automatically creates a list of compute node names and uses them to populate a genders group called nodes. This genders file can be found at `/opt/flight/etc/genders`.

Users can find the names of their compute nodes by using the `nodeattr` command; e.g.

- `nodeattr -s nodes`
    - shows a space-separated list of current compute node hostnames<br><br>
- `nodeattr -c nodes`
    - shows a comma-separated list of current compute node hostnames<br><br>
- `nodeattr -n nodes`
    - shows a new-line-separated list of current compute node hostnames