---
order: 90
label: Installing Flight User Suite
icon: dot
---


The OpenFlight project packages tools as both RPMs and debs that are hosted in package repositories which can be quickly installed with a couple of commands. These need to be set up before the User Suite can be installed.

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
sudo dnf config-manager --set-enabled powertools
```

- Most tools require packages available in the EPEL repository, installing it is recommended:

```bash
sudo dnf install epel-release
```

- Finally, rebuild the yum cache:
```bash
sudo dnf makecache
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



!!!
There are 3 repositories available - production (enabled by default), dev (providing development releases of tools) and vault (access to old, unsupported versions and retired tools).
!!!




## Installing the User Suite

The quickest and simplest way to get up and running with the user suite is to simply install the group package for the tools. This will ensure that compatible versions of all the tools are installed.

+++ CentOS 7

- Install the user suite RPM:
```bash
sudo yum install flight-user-suite
```
+++ CentOS 8

- Install the user suite RPM:
```bash
sudo dnf install flight-user-suite
```
+++ Ubuntu 18.04

- Install the user suite deb:
```bash
sudo apt-get install flight-user-suite
```
+++ Ubuntu 20.04

- Install the user suite deb:
```bash
sudo apt-get install flight-user-suite
```
+++



!!!
After installation, either reboot your system or logout and back in again to expose the `flight` command to the shell
!!!