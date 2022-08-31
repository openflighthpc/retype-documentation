---
order: 70
label: Requesting a longer runtime
icon: dot
---

In order to promote best-use of the research environment scheduler, particularly in a shared environment, it is recommend to inform the scheduler the amount of time the submitted job is expected to take. You can inform the research environment scheduler of the expected runtime using the `-t, --time=<time>` option. For example - to submit a job that runs for 2 hours, the following example job script could be used:

```bash
#!/bin/bash -l
#SBATCH --job-name=sleep
#SBATCH -D $HOME/
#SBATCH --time=0-2:00
sleep 7200
```

You can then see any time limits assigned to running jobs using the command `squeue --long`:

```bash
[centos@chead1 (mycluster1) ~]$ squeue --long
Tue Aug 30 10:55:55 2016
             JOBID PARTITION     NAME     USER    STATE       TIME TIME_LIMI  NODES NODELIST(REASON)
              1163       all    sleep    centos  RUNNING       0:07   2:00:00      1 ip-10-75-1-42
```

