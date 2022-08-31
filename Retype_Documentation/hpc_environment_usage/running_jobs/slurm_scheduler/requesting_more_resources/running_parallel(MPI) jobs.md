---
order: 90
label: Running Parallel (MPI) jobs
icon: dot
---

If users want to run parallel jobs via a messaging passing interface (MPI), they need to inform the scheduler - this allows jobs to be efficiently spread over compute nodes to get the best possible performance. Using multiple CPU cores across multiple nodes is achieved by specifying the `-N` or `--nodes=<minnodes[-maxnodes]>` option - which requests a minimum (and optional maximum) number of nodes to allocate to the submitted job. If _only_ the `minnodes` count is specified - then this is used for both the minimum _and_ maximum node count for the job.

`--nodes=1-4`

Example of how to request a minimum of 1 node and maximum of 4.

You can request multiple cores over multiple nodes using a combination of scheduler directives either in your job submission command or within your job script. Some of the following examples demonstrate how you can obtain cores across different resources;

`--nodes=2 --ntasks=16`

   Requests 16 cores across 2 compute nodes

`--nodes=2`

   Requests all available cores of 2 compute nodes

`--ntasks=16`

   Requests 16 cores across any available compute nodes

For example, to use 64 CPU cores on the research environment for a single application, the instruction `--ntasks=64` can be used. The following example shows launching the **Intel Message-passing** MPI benchmark across 64 cores on your research environment. This application is launched via the OpenMPI `mpirun` command - the number of threads and list of hosts are automatically assembled by the scheduler and passed to the MPI at runtime. This jobscript loads the `apps/imb` module before launching the application, which automatically loads the module for **OpenMPI**.

```bash
#!/bin/bash -l
#SBATCH -n 64
#SBATCH --job-name=imb
#SBATCH -D $HOME/
#SBATCH --output=imb.out.%j
module load apps/imb
mpirun --prefix $MPI_HOME \
       IMB-MPI1
```

We can then submit the IMB job script to the scheduler, which will automatically determine which nodes to use:

```bash
[flight@chead1 (mycluster1) ~]$ sbatch imb.sh
Submitted batch job 1162
[flight@chead1 (mycluster1) ~]$ squeue
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
                           1162       all      imb    centos  R       0:01      8 ip-10-75-1-[42,45,62,67,105,178,233,250]
[flight@chead1 (mycluster1) ~]$ cat imb.out.1162
#------------------------------------------------------------
#    Intel (R) MPI Benchmarks 4.0, MPI-1 part
#------------------------------------------------------------
# Date                  : Tue Aug 30 10:34:08 2016
# Machine               : x86_64
# System                : Linux
# Release               : 3.10.0-327.28.3.el7.x86_64
# Version               : #1 SMP Thu Aug 18 19:05:49 UTC 2016
# MPI Version           : 3.0
# MPI Thread Environment:

#---------------------------------------------------
# Benchmarking PingPong
# #processes = 2
# ( 62 additional processes waiting in MPI_Barrier)
#---------------------------------------------------
       #bytes #repetitions      t[usec]   Mbytes/sec
            0         1000         3.17         0.00
            1         1000         3.20         0.30
            2         1000         3.18         0.60
            4         1000         3.19         1.19
            8         1000         3.26         2.34
           16         1000         3.22         4.74
           32         1000         3.22         9.47
           64         1000         3.21        19.04
          128         1000         3.22        37.92
          256         1000         3.30        73.90
          512         1000         3.41       143.15
         1024         1000         3.55       275.36
         2048         1000         3.75       521.04
         4096         1000        10.09       387.14
         8192         1000        11.12       702.51
        16384         1000        12.06      1296.04
        32768         1000        14.65      2133.32
        65536          640        19.30      3238.72
       131072          320        29.50      4236.83
       262144          160        48.17      5189.77
       524288           80        84.36      5926.88
      1048576           40       157.40      6353.32
      2097152           20       305.00      6557.31
      4194304           10       675.20      5924.16
```

!!!
If you request more CPU cores than your research environment can accommodate, your job will wait in the queue.
!!!


