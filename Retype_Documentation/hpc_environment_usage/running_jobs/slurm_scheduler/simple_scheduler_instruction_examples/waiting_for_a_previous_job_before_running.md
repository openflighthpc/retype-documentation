---
order: 80
label: Waiting for a previous job before running
icon: dot
--- 

You can instruct the scheduler to wait for an existing job to finish before starting to run the job you are submitting with the `-d [state:job_id] | --depend=[state:job_id]` option. For example, to wait until the job with ID 75 has finished before starting the job, you could use the following syntax:

```bash
[centos@gateway1 (mycluster1) ~]$ squeue
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
                75       all    myjob    centos  R       0:01      1 node01

[centos@gateway1 (mycluster1) ~]$ sbatch --dependency=afterok:75 mytestjob.sh
Submitted batch job 76

[centos@gateway1 (mycluster1) ~]$ squeue
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
                76       all    myjob    centos PD       0:00      1 (Dependency)
                75       all    myjob    centos  R       0:15      1 node01
```