---
order: 100
label: Setting output file location
icon: dot
---

To set the output file location for your job, use the `-o [file_name] | --output=[file_name]` option - both standard-out and standard-error from your job-script, including any output generated by applications launched by your job-script will be saved in the filename you specify.

By default, the scheduler stores data relative to your home-directory - but to avoid confusion, we recommend **specifying a full path to the filename** to be used. Although Linux can support several jobs writing to the same output file, the result is likely to be garbled - it’s common practice to include something unique about the job (e.g. its job-ID) in the output filename to make sure your job’s output is clear and easy to read.

!!!
The directory used to store your job output file must exist and be writable by your user before you submit your job to the scheduler. Your job may fail to run if the scheduler cannot create the output file in the directory requested.
!!!

The following example uses the `--output=[file_name]` instruction to set the output file location:

```bash
#!/bin/bash -l
#SBATCH --job-name=myjob --output=output.%j

echo "Starting running on host $HOSTNAME"
sleep 120
echo "Finished running - goodbye from $HOSTNAME"
```

In the above example, assuming the job was submitted as the `centos` user and was given the job-ID number `24`, the scheduler will save the output data from the job in the filename `/home/centos/output.24`.
