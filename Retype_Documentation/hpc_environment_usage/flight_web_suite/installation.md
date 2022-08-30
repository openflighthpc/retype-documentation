---
order: 120
label: Installation
icon: dot
---

+++ Centos 7

To install the flight web suite:

```bash
sudo yum install flight-web-suite
```
+++ Centos 8
To install the flight web suite:

```bash
sudo yum install flight-web-suite
```
+++ Ubuntu 18.04
To install the flight web suite:

```bash
sudo apt install flight-web-suite
```

+++ Ubuntu 20.04

To install the flight web suite:

```bash
sudo apt install flight-web-suite
```
+++

Once installed, enable all web services:

```
flight web-suite enable
```

And then start:

```bash
flight web-suite start
```

## Connecting to Web Suite

Navigate to the external IP or hostname for the gateway. e.g. `https://<ip address>`

If the http page works, but https doesn't, you may need to enable https:

```bash
flight www enable-https
```

## Logging in

Log in with the same user details used for accessing the cluster from a CLI. If you find yourself being logged out when changing pages, you may need to add 





2.5 Flight Web Suite

2.5.1 What is Flight Web Suite?

The Flight Web Suite is a collection of web applications that provide users with easy and intuitive ways to interact with
their research environment. The purpose of these tools is to get researchers started with HPC as quickly as possible
without needing to worry about configuring system access and desktop session creation, leaving them to do what they
do best - research!

Flight Web Suite is made up of the following tools:

- WWW: Flight WWW provides a standalone NGINX server preconfigured to host the various web suite applications
- Certbot: Flight Certbot provides helper tools for Flight Web Suite
- Service: Flight Service provides management of the various web applications and services
- Console WebApp/API: The API & web application for accessing terminals via a browser
- Desktop WebApp/API: The API & web application for creating, managing & using desktops via a browser
- File Manager WebApp/API: The API & web application for managing user files via a browser
- Job Script WebApp/API: The API & web application for templating, creating, submitting & managing job
scripts via a browser

2.5.2 Installing Flight Web Suite

The OpenFlight project packages tools as both RPMs and debs that are hosted in package repositories which can be
quickly installed with a couple of commands.
Before proceeding, ensure that the Flight User Suite is installed.

Installation Method 1: Quick
The quickest and simplest way to get up and running with the user suite is to simply install the group package for the
tools. This will ensure that compatible versions of all the tools are installed.






+++ CentOS 7
- Install the web suite:
```bash
[flight@gateway1 ~]$ sudo yum install flight-web-suite
```
- Set the domain name (for use with certificate generation, this can be either a hostname or IP. A publicly acces-
sible value should be used if intending to use Lets Encrypt certificates):
```bash
[flight@gateway1 ~]$ flight web-suite set-domain gateway1.scooby.example.com
```
- Install extra packages (note: the EPEL repository is required for the websockify package):
```bash
[flight@gateway1 ~]$ sudo yum install python-websockify xorg-x11-apps netpbm-progs
```
- Restart the web-suite to apply changes:
```bash
[flight@gateway1 ~]$ flight web-suite restart
```

+++ CentOS 8
- Install the web suite RPM:
```bash
[flight@gateway1 ~]$ sudo dnf install flight-web-suite
```
- Install extra packages (note: the PowerTools repository is required for the xorg-x11-apps package):
```bash
[flight@gateway1 ~]$ sudo dnf install python3-websockify xorg-x11-apps netpbm-progs
```
+++ Ubuntu 18.04

- Install the web suite deb:
```bash
flight@gateway1:~$ sudo apt-get install flight-web-suite
```
- Install extra packages:
```bash
flight@gateway1:~$ sudo apt-get install netpbm x11-apps websockify
```

+++ Ubuntu 20.04

- Install the web suite deb:
```bash
flight@gateway1:~$ sudo apt-get install flight-web-suite
```
- Install extra packages:
```bash
flight@gateway1:~$ sudo apt-get install netpbm x11-apps websockify
```

+++

Installation Method 2: Manual

For those who wish to have more control over their installation, all of the Flight User Suite tools have manual instal-
lation instructions in the READMEs on GitHub.
- Flight WWW - https://github.com/openflighthpc/openflight-omnibus-builder/tree/master/builders/flight-www
- Flight Certbot - https://github.com/openflighthpc/openflight-omnibus-builder/tree/master/builders/flight-certbot
- Flight Service - https://github.com/openflighthpc/openflight-omnibus-builder/tree/master/builders/
flight-service
- Flight Console API - https://github.com/openflighthpc/flight-console-api#installation
- Flight Console WebApp - https://github.com/openflighthpc/flight-console-webapp#installation
- Flight Desktop API - https://github.com/openflighthpc/flight-desktop-restapi#installation
- Flight Desktop WebApp - https://github.com/openflighthpc/flight-desktop-webapp#installation


2.5.3 Configuring Web Suite
System Prerequisites
In order to authenticate the user in the web interface, the following must be true:
- User has a password (can be set with the passwd command or through other user management software that is
setup on the system)
- Ports 80 & 443 on the gateway must be accessible (allowed through both the system firewall and cloud security
group)
- SSH password authentication must be enabled (can be set in /etc/ssh/sshd_config in CentOS or through
other access management software that is setup on the system)
Certificate Preparation
To secure the server connections, it is recommended to generate a certificate to be used by the web suite. The Flight
Web Suite comes with tools that can generate either a “self-signed” or LetsEncrypt certificate. Alternatively, a certifi-
cate that has been created outside of the web suite can be used to secure the server.


 
Self-Signed
A self-signed certificate, whilst not usually trusted by browsers, does still provide extra security to the web server over
HTTP communication.
A self-signed certificate is automatically created when installing the packages from the repo.
To generate and install the self-signed certificates, simply:
```bash
[flight@gateway1(scooby) ~]$ flight www cert-gen --cert-type self-signed --domain
˓→$(hostname -f)
```
After this has run, changes are applied on a service restart:
```bash
[flight@gateway1(scooby) ~]$ flight web-suite restart
```
Lets Encrypt

To generate and install a Lets Encrypt certificate, run the following (replacing the domain and email with appropriate
values):
```bash
[flight@gateway1(scooby) ~]$ flight www cert-gen --cert-type lets-encrypt --domain
˓→gateway1.scooby.example.com --email user@example.com
```

!!!
Ensure that the domain/IP is publicly accessible in order for certificate generation to work
!!!

After this has run, changes are applied on a service restart:
```bash
[flight@gateway1(scooby) ~]$ flight web-suite restart
```
External Certificate
Externally generated certificates can be used by placing them in /opt/flight/etc/www/ssl/, the files that
should be in there are:
- fullchain.pem: The full certificate (recommended permissions are 644 root:root)
- key.pem: The private key for the certificate (recommended permissions are 644 root:root)
After placing the certificates in place, the HTTPS server can be enabled with:

```bash
[flight@gateway1(scooby) ~]$ flight web-suite restart
```