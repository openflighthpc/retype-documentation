---
order: 100
label: Preparing a Desktop Type
icon: dot
---

On the previous page, some application types were `unverified`, these need to be prepared before they can be verified.

To prepare a new session type, use the command `flight desktop prepare <type>` (preparing will automatically install any required application and support files, if these dependencies have been installed manually then a desktop session can be checked for verfication with `flight desktop verify <type>`). Once enabled, users can start a new session using the command `flight desktop start <type>`.

!!!
The `prepare` command is only available to the `root` user as it requires installation of packages
!!!

!!!
Preparing a new session type only enables it for the machine that you run the command from, any other nodes will need to have the type enabled too.
!!!

## Using sudo to prepare

Since only the root user can use `prepare`, you also cannot use `sudo` to run `prepare`.

Instead the user must become a root user with the command:

`sudo su -`

With this the user becomes a root user, and must run flight again with `flight start`.

Now the command to prepare a session type can be run.

Root user mode can be exited by running the command `exit`, `logout`, or by pressing **Ctrl** + **D**.



