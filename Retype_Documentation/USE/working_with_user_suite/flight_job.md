---
order: 80
label: Flight Job
icon: 
---


# Flight Job


The Flight User Suite comes with a utility to jumpstart running jobs on the research environment. This tool provides preconfigured script templates. 

## Showing Available Job Scripts

To show the available guides, list them with:

    [flight@gateway1 (scooby) ~]$ flight job list
    â”Œâ”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
    â”‚ Index â”‚ Name            â”‚
    â”œâ”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
    â”‚ 1     â”‚ mpi-nodes.sh    â”‚
    â”‚ 2     â”‚ mpi-slots.sh    â”‚
    â”‚ 3     â”‚ simple.sh       â”‚
    â”‚ 4     â”‚ simple-array.sh â”‚
    â”‚ 5     â”‚ smp.sh          â”‚
    â””â”€â”€â”€â”€â”€â”€â”€â”´â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜


## Viewing Script Information


The various job scripts have descriptions that explain the purpose of the template. 

To view the description of a job script:

```bash
[flight@gateway1 (scooby) ~]$ flight job info 1
mpi-nodes.sh - MPI multiple node (Slurm)

  DESCRIPTION

  Submit a single job that spans multiple nodes where you want exclusive use of each node allocated.

  LICENSE

  This work is licensed under a Creative Commons Attribution-ShareAlike 4.0 International License.

  COPYRIGHT

  Copyright (C) 2020 Alces Flight Ltd.
```

!!!
The script can be referred to by its name or index
!!!

## Copying Job Script


The job utility provides helpers to create copies of the various scripts. To copy a script to the current directory:

```bash
[flight@gateway1 (scooby) ~]$ flight job cp 2
Successfully copied the template to: /home/flight/mpi-slots.sh
```

!!!
The script can be referred to by its name or index
!!!

Further control over the copying & naming of the file, following the cp command with a path/name will copy the script as such:

```bash
[flight@gateway1 (scooby) ~]$ flight job cp 4 myjob/run.sh
Successfully copied the template to: /home/flight/myjob/run.sh
```

!!!
If the output directory doesn't exist then ``flight job`` will attempt to create it
!!!
