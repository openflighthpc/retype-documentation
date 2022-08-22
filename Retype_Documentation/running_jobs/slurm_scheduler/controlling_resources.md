---
order: 50
label: Controlling resources
icon: dot
---

In order to promote efficient usage of the research environment - the job-scheduler is automatically configured with default run-time limits for jobs. These defaults can be overridden by users to help the scheduler understand how you want it to run your job. 

Job instructions can be provided in two ways; they are:

1. **On the command line**, as parameters to your `sbatch` or `srun` command. For example, you can set the name of your job using the `--job-name=[name] | -J [name]` option:

```bash
[centos@gateway1 (mycluster1) ~]$ sbatch --job-name=mytestjob simplejobscript.sh
Submitted batch job 51

[centos@gateway1 (mycluster1) ~]$ squeue
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
                51       all mytestjo    centos  R       0:02      1 node01
```

2. **In your job script**, by including scheduler directives at the top of your job script - you can achieve the same effect as providing options with the `sbatch` or `srun` commands. Create an example job script or modify your existing script to include a scheduler directive to use a specified job name:

```bash
#!/bin/bash -l
#SBATCH --job-name=mytestjob
echo "Starting running on host $HOSTNAME"
sleep 120
echo "Finished running - goodbye from $HOSTNAME"
```

Including job scheduler instructions in your job-scripts is often the most convenient method of working for batch jobs - follow the guidelines below for the best experience:

- Lines in your script that include job-scheduler directives must start with `#SBATCH` at the beginning of the line.
- You can put multiple instructions separated by a space on a single line starting with `#SBATCH`
- The scheduler will parse the script from top to bottom and set instructions in order; if you set the same parameter twice, the second value will be used.
- Instructions are parsed at job submission time, before the job itself has actually run. This means you can’t, for example, tell the scheduler to put your job output in a directory that you create in the job-script itself - the directory will not exist when the job starts running, and your job will fail with an error.
- You can use dynamic variables in your instructions (see next)


!!!warning
After `#!/bin/bash -l` write all of your `#SBATCH` lines. As soon as the interpreter reads a normal script line it will stop looking for `#SBATCH` lines.
!!!

[More information on this](https://slurm.schedmd.com/sbatch.html#SECTION_DESCRIPTION)
