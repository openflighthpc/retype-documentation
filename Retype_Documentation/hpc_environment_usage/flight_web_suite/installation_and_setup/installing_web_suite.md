---
order: 90
label: Installing Web Suite
icon: dot-fill
---

The OpenFlight project packages tools as both RPMs and debs that are hosted in package repositories which can be
quickly installed with a couple of commands.
Before proceeding, ensure that the Flight User Suite is installed.

## Installation Method 1: Quick
The quickest and simplest way to get up and running with the user suite is to simply install the group package for the
tools. This will ensure that compatible versions of all the tools are installed.




+++ CentOS 7
- Install the web suite:
```bash
sudo yum install flight-web-suite
```
- Set the domain name (for use with certificate generation, this can be either a hostname or IP. A publicly accessible value should be used if intending to use Lets Encrypt certificates):
```bash
flight web-suite set-domain gateway1.mycluster1.example.com
```
- Install extra packages (note: the EPEL repository is required for the websockify package):
```bash
sudo yum install python-websockify xorg-x11-apps netpbm-progs
```
- Restart the web-suite to apply changes:
```bash
flight web-suite restart
```

+++ CentOS 8
- Install the web suite RPM:
```bash
sudo dnf install flight-web-suite
```
- Install extra packages (note: the [Power Tools](http://localhost:5000/hpc_environment_usage/flight_overview/installing_flight_user_suite/adding_the_openflight_package/#centos-8) repository is required for the xorg-x11-apps package):
```bash
sudo dnf install python3-websockify xorg-x11-apps netpbm-progs
```
+++ Ubuntu 18.04

- Install the web suite deb:
```bash
sudo apt-get install flight-web-suite
```
- Install extra packages:
```bash
sudo apt-get install netpbm x11-apps websockify
```

+++ Ubuntu 20.04

- Install the web suite deb:
```bash
sudo apt-get install flight-web-suite
```
- Install extra packages:
```bash
sudo apt-get install netpbm x11-apps websockify
```

+++



## Installation Method 2: Manual

For those who wish to have more control over their installation, all of the Flight User Suite tools have manual installation instructions in the READMEs on GitHub.
- Flight WWW - https://github.com/openflighthpc/openflight-omnibus-builder/tree/master/builders/flight-www
- Flight Certbot - https://github.com/openflighthpc/openflight-omnibus-builder/tree/master/builders/flight-certbot
- Flight Service - https://github.com/openflighthpc/openflight-omnibus-builder/tree/master/builders/flight-service
- Flight Console API - https://github.com/openflighthpc/flight-console-api#installation
- Flight Console WebApp - https://github.com/openflighthpc/flight-console-webapp#installation
- Flight Desktop API - https://github.com/openflighthpc/flight-desktop-restapi#installation
- Flight Desktop WebApp - https://github.com/openflighthpc/flight-desktop-webapp#installation
