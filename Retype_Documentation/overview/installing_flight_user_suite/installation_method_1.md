---
order: 90
label: "Installation Method 1: Quick"
icon: dot
---


The quickest and simplest way to get up and running with the user suite is to simply install the group package for the tools. This will ensure that compatible versions of all the tools are installed.

+++ CentOS 7

- Install the user suite RPM:
```bash
[flight@gateway1 ~]$ sudo yum install flight-user-suite
```
+++ CentOS 8

- Install the user suite RPM:
```bash
[flight@gateway1 ~]$ sudo dnf install flight-user-suite
```
+++ Ubuntu 18.04

- Install the user suite deb:
```bash
flight@gateway1:~$ sudo apt-get install flight-user-suite
```
+++ Ubuntu 20.04

- Install the user suite deb:
```bash
flight@gateway1:~$ sudo apt-get install flight-user-suite
```
+++

!!!
After installation, either reboot your system or logout and back in again to expose the `flight` command to the shell
!!!