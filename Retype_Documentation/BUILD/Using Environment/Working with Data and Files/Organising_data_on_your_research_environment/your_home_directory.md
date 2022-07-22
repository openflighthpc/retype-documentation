---
order: 90
label: Your home directory
icon: dot
---

The shared filesystem includes the home-directory area for the `flight` user which is created when your research environment is launched. Linux automatically places users in their home-directory when they login to a node. By default, Flight Compute will create your home-directory under the `/users/` directory, named `flight` (`/users/flight`).

The Linux command line will accept the `~` (tilde) symbol as a substitute for the currently logged-in users’ home-directory. The environment variable `$HOME` is also set to this value by default. Hence, the following three commands are all equivalent when logged in as the user flight:

- `ls /users/flight`
- `ls ~`
- `ls $HOME`

The root user in Linux has special meaning as a privileged user, and does not have a shared home-directory across the research environment. The root account on all nodes has a home-directory in `/root`, which is separate for every node. For security reasons, users are not permitted to login to a node as the root user directly - please login as a standard user and use the `sudo` command to get privileged access.