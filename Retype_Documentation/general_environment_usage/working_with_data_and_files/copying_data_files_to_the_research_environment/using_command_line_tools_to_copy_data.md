---
order: 100
label: Using command-line tools to copy data
icon: dot-fill
---

The research environment login node is accessible via SSH, allowing use of the `scp` and `sftp` commands to transfer data from your local client machine.


+++ Linux/Mac

Linux and Mac users can use in-built SSH support to copy files. To copy file mydata.zip to your research environment on IP address 52.48.62.34, use the command:

`scp -i mykeyfile.pem mydata.zip flight@52.48.62.34:.`

- replace mykeyfile.pem with the name of your SSH public key
- replace flight with your username on the research environment

+++ Windows

Windows users can download and install the [pscp](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) command to perform the same operation (for this you will need your .pem key in .ppk format, see [connecting from Windows with Putty](/general_environment_usage/cli_basics/logging_in/#logging-in)):

`pscp -i mykeyfile.ppk mydata.zip flight@52.48.62.34:/users/flight/.`
+++

SCP/PSCP

Both the `scp` and the `pscp` commands take the parameter `-r` to recursively copy entire directories of files to the research environment.

To retrieve files from the research environment, simply specify the location of the remote file first in the scp command, followed by the location on the local system to put the file; e.g.

To copy file myresults.zip from your research environment on IP address 52.48.62.34 to your local Linux or Mac client:

    scp -i mykeyfile.pem flight@52.48.62.34:/users/flight/myresults.zip .

