---
order: 100
label: Local Jobs
icon: dot
---



## Why Run a Local Job?

When using a personal research environment there isn’t a need to monitor resource usage as closely as multi-user systems where miscommunication and overloaded resources can negatively impact research progress. With all the resources available to one user it is quicker and easier to run jobs simply through a terminal than using a queue system.

Local jobs also have the benefit over schedulers by launching immediately and providing all output through a single terminal.

## Running a Local Job

Local job scripts can be written in any language supported within the research environment. In most cases this is likely to be bash as it’s a flexible and functional shell scripting language which enables users to intuitely navigate the filesystem, launch applications and manage data output.

In the event that a job script is executable, contains a shebang(#!) specifying the launch language, and is in the current directory, it’s as simple to run as:

```bash
[flight@chead1 ~]$ ./myjob.sh
```
   
