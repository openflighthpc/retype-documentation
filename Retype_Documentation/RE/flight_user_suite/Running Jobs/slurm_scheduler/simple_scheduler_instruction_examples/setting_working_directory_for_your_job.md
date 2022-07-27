---
order: 90
label: Setting working directory for your job
icon: dot
---

By default, jobs are executed from your home-directory on the research environment (i.e. `/home/<your-user-name>`, `$HOME` or `~`). You can include `cd` commands in your job-script to change to different directories; alternatively, you can provide an instruction to the scheduler to change to a different directory to run your job. The available options are:

`-D | --workdir=[dir_name]` - instruct the job scheduler to move into the directory specified before starting to run the job on a compute node

!!!
The directory specified must exist and be accessible by the compute node in order for the job you submitted to run.
!!!