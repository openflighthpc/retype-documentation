---
order: 100
label: Adding the Openflight Package
icon: dot-fill
---
## Installing Flight User Suite

The OpenFlight project packages tools as both RPMs and debs that are hosted in package repositories which can be quickly installed with a couple of commands. 

### Adding the OpenFlight Package Repositories

+++ CentOS 7

- Install the OpenFlight release RPM:

```bash
sudo yum install https://repo.openflighthpc.org/pub/centos/7/openflighthpc-release-latest.noarch.rpm
```
- Rebuild the yum cache:
```bash
sudo yum makecache
```
!!!
Some tools require packages available in the EPEL repository, this can be installed with `sudo yum install epel-release`
!!!

+++ CentOS 8

- Install the OpenFlight release RPM:
```bash
sudo dnf install https://repo.openflighthpc.org/openflight/centos/8/x86_64/openflighthpc-release-3-1.noarch.rpm
```

- Add the Power Tools repository:

```bash
sudo yum config-manager --set-enabled powertools
```

- Most tools require packages available in the EPEL repository, installing it is recommended:

```bash
sudo yum install epel-release
```

- Finally, rebuild the yum cache:
```bash
sudo yum makecache
```

+++ Ubuntu 18.04

- Import the public signature for OpenFlight:
```bash
sudo apt-key adv --fetch-keys https://repo.openflighthpc.org/openflighthpc-archive-key.asc
```
- Install the OpenFlight repository:
```bash
sudo apt-add-repository "deb https://repo.openflighthpc.org/openflight/ubuntu stable main"
```
- Update the apt cache:
```bash
sudo apt-get update
```
+++ Ubuntu 20.04

- Import the public signature for OpenFlight:
```bash
sudo apt-key adv --fetch-keys https://repo.openflighthpc.org/openflighthpc-archive-key.asc
```
- Install the OpenFlight repository:
```bash
sudo apt-add-repository "deb https://repo.openflighthpc.org/openflight/ubuntu stable main"
```
- Update the apt cache:
```bash
sudo apt-get update
```
+++

Now the OpenFlight repositories are installed. There are 3 repositories available - production (enabled by default), dev (providing development releases of tools) and vault (access to old, unsupported versions and retired tools).
