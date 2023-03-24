---
order: -10
label: Using Flight Job (CLI)
icon: dot
---



## Showing Available Job Scripts

To show the available guides, list them with:

```bash
[flight@chead1 (mycluster1) ~]$ flight job list-templates

┌───────┬─────────────────────────┬─────────────────────────────────────────────┐
│ Index │ ID                      │ Name                                        │
├───────┼─────────────────────────┼─────────────────────────────────────────────┤
│ 1     │ desktop-on-login-node   │ Interactive desktop session on login node   │
│ 2     │ desktop-on-compute-node │ Interactive desktop session on compute node │
│ 3     │ simple                  │ Simple serial                               │
│ 4     │ simple-array            │ Simple serial array                         │
│ 5     │ mpi-slots               │ Multiple slot                               │
│ 6     │ mpi-nodes               │ Multiple node                               │
│ 7     │ smp                     │ SMP multiple slot                           │
└───────┴─────────────────────────┴─────────────────────────────────────────────┘
```

## Viewing Script Information


The various job scripts have descriptions that explain the purpose of the template. 

To view the description of a job script:

```bash
[flight@chead1 (mycluster1) ~]$ flight job info-template 1
      ID: desktop-on-login-node
    Name: Interactive desktop session on login node
Synopsis: Start an interactive desktop session on a login node and submit a job to run on a compute node.

DESCRIPTION:
An interactive desktop session will start on a login node.  Once that
session is running, resources will be requested from the scheduler to run
the job script.  If the job script starts a graphical application it will be
available from inside the desktop session.
```

!!!
The script can be referred to by its name or index
!!!

## Copying Job Script


The job utility provides helpers to create copies of the various scripts. To copy a script to the current directory:

```bash
[flight@chead1 (mycluster1) ~]$ flight job copy-template 1
Successfully copied the template to: /home/flight/interactive-desktop.sh.1
```

!!!
The script can be referred to by its name or index
!!!

Further control over the copying & naming of the file, following the cp command with a path/name will copy the script as such:

```bash
[flight@chead1 (mycluster1) ~]$ flight job copy-template 1 $HOME/spam
Successfully copied the template to: /home/flight/spam/interactive-desktop.sh
```

!!!
If the output directory doesn't exist then ``flight job`` will attempt to create it
!!!
