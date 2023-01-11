---
order: 30
label: '3\. Testing a Standalone Cluster configuration'
icon: dot
---



After the creation and configuration of nodes has been complete, everything should work. Here is a test for every cluster type to confirm this.

+++ Slurm

1. Create a file called `simplejobscript.sh`, and copy this into it:
    ```
    #!/bin/bash -l
    echo "Starting running on host $HOSTNAME"
    sleep 30
    echo "Finished running - goodbye from $HOSTNAME"
    ```
    This is just a simple script that sends some messages and sleeps for 30 seconds

2. Run the script with `sbatch simplejobscript.sh`.

3. The job should start and complete without issues.
+++