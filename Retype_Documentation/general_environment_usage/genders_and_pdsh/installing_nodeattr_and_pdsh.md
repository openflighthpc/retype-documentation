---
order: 100
label: Installing nodeattr and pdsh
icon: dot
---

A combination of genders and pdsh can allow for management and monitoring of multiple nodes at a time. OpenFlight provides a build of PDSH that integrates with the rest of the User Suite.

Nodeattr and pdsh can be installed using the yum package manager, simply:

```bash
sudo yum -y install flight-pdsh
```

Once installed, the pdsh command will be available to active [OpenFlight User Suite](/hpc_environment_usage/flight_overview/what_is_flight_user_suite/#what-is-the-flight-user-suite) sessions. The priority of the OpenFlight pdsh command in the path can be configured with:

```bash
flight config set pdsh.priority X
```

Where `X` is one of:

- `system` - Prefer system PDSH
- `embedded` - Prefer OpenFlight PDSH
- `disabled` - Do not include OpenFlight PDSH in PATH

!!!
OpenFlight PDSH defaults `system` priority, to ensure that the OpenFlight User Environment uses the OpenFlight PDSH, set the priority to `embedded` after installation (`flight config set pdsh.priority embedded`)
!!!
