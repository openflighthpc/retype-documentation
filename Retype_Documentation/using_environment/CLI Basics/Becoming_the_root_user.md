---
order: 0
label: Becoming the root user
icon: dot
---

Most research environment operations, including starting applications and running jobs, should be performed as the user created when the Flight User Suite research environment was launched from the launch template. However - for some privileged operations, users may need to change to being the root user. Users can prefix any command they want to run as the root user with the `sudo` command; e.g.

`sudo yum install screen`

For security reasons, SSH login as the root user is not permitted to a Flight Compute environment. To get a Linux shell with root privileges, please login as your standard user then execute the command `sudo -s`.


!!!warning
Users must exercise caution when running commands as root, as they have the potential to disrupt research environment operations.
!!!