---
order: 80
label: SLURM
icon: dot-fill
---

Via Flight, SLURM schedules interactive and batch jobs. To test its functionality:



1. Run an interactive job:
    ```
    srun --pty /bin/bash
    ```
    If all was successful, the command prompt should have changed to the node running the interactive job. E.g.
    ```
    [flight@chead1 (mycluster1) ~]$ srun --pty /bin/bash
    [flight@cnode01 ~]$ 
    ```
    Exit the interactive job with `exit`.
    
2. Run a batch job:
    - Create a file called job-test.sh with this inside:
        ```bash
        #!/bin/bash -l
        echo "Starting running on host $HOSTNAME"
        sleep 12
        echo "Finished running - goodbye from $HOSTNAME"
        ```
    - Run that job:
        ```
        sbatch job-test.sh
        ```

3. Within 10 seconds of running the job, check to see if it is running:
    ```
    squeue
    ```
    If this functions, there should be a table of running jobs, one of which should be job-test.sh. E.g.

    ```
    [flight@chead1 (mycluster1) ~]$ squeue
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
                 4       all job-test   flight  R       0:01      1 cnode01
    ```

4. Wait for the job from step 2 to finish. Check the output file, which will be in the same directory that the job was run from. If successful it will look like this:
    ```
    [flight@chead1 (mycluster1) ~]$ cat slurm-4.out
    Starting running on host cnode01.pri.mycluster1.cluster.local
    Finished running - goodbye from cnode01.pri.mycluster1.cluster.local
    ```
    If the output file shows an error, then the job was not successful.

5. Run another job, and then cancel it:
    ```
    scancel <job-ID>
    ```
    If successful the job's output file should show that it was cancelled.

6. Check available nodes:
    ```
    sinfo -Nl 
    ```
    If successful, all the nodes that are expected to be available will be shown. E.g.
    ```
    [flight@chead1 (mycluster1) ~]$ sinfo -Nl
    Wed Oct 12 14:29:07 2022
    NODELIST   NODES PARTITION       STATE CPUS    S:C:T MEMORY TMP_DISK WEIGHT AVAIL_FE REASON              
    cnode01        1      all*        idle 1       1:1:1      1        0      1   (null) none                
    ```

