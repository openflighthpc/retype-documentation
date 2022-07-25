---
order: 100
label: Preparing a Desktop Type
---

To prepare a new session type, use the command `flight desktop prepare <type>` (preparing will automatically install any required application and support files, if these dependencies have been installed manually then a desktop session can be checked for verfication with `flight desktop verify <type>`). Once enabled, users can start a new session using the command `flight desktop start <type>`.

!!!
The `prepare` command is only available to the `root` user as it requires installation of packages
!!!

!!!
Preparing a new session type only enables it for the machine that you run the command from, any other nodes will need to have the type enabled too.
!!!

