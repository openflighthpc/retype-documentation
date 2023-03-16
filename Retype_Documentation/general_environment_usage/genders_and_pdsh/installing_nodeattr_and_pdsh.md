---
order: 100
label: Installing nodeattr and pdsh
icon: dot
---

Flight Solo comes pre-installed with the Openflight build of pdsh, so installation won't be necessary if using it.

### Installing

+++ Centos 7
Nodeattr and pdsh can be installed using the yum package manager, simply:

```bash
sudo yum -y install flight-pdsh
```
+++ Centos 8
Nodeattr and pdsh can be installed using the yum package manager, simply:

```bash
sudo dnf -y install flight-pdsh
```

+++ Ubuntu 18.04
Nodeattr and pdsh can be installed using the apt package manager, simply:

```bash
sudo apt -y install flight-pdsh
```
+++ Ubuntu 20.04
Nodeattr and pdsh can be installed using the apt package manager, simply:

```bash
sudo apt -y install flight-pdsh
```
+++

Once installed, the pdsh command will be available to active [OpenFlight User Suite](/flight_environment_usage/#what-is-the-flight-user-suite) sessions. The priority of the OpenFlight pdsh command in the path can be configured with:

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
