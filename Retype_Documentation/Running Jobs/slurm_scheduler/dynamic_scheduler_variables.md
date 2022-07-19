---
order: 40
label: Dynamic scheduler variables
---


Your research environment job scheduler automatically creates a number of pseudo environment variables which are available to your job-scripts when they are running on research environment compute nodes, along with standard Linux variables. Useful values include the following:

- `$HOME` The location of your home-directory
- `$USER` The Linux username of the submitting user
- `$HOSTNAME` The Linux hostname of the compute node running the job
- `%a / $SLURM_ARRAY_TASK_ID` Job array ID (index) number. The `%a` substitution should only be used in your job scheduler directives
- `%A / $SLURM_ARRAY_JOB_ID` Job allocation number for an array job. The %A substitution should only be used in your job scheduler directives
- `%j / $SLURM_JOBID` Job allocation number. The `%j` substitution should only be used in your job scheduler directives
