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

+++ Jupyter

Put the IP/FQDN used in configuration into your browser to access the [Flight Web Suite](/flight_environment_usage/flight_web_suite/). It should look something like this:
![](/images/websuite_home_jupyter.png)

Under "Quick Access" click on "Jupyter" and enter the password set during configuration when requested; it will only need to be entered the first time you connect.
![](/images/websuite_jupyter_password.png)

On the Jupyter home page, under the "Notebook" section, click on "Python3" to open a new notebook.

![](/images/websuite_jupyter_newpython.png)

Enter this code, which will print out a message, wait for a bit, then print again.
```
import time
print("Starting running on Jupyter")
time.sleep(3)
print("Finished running - goodbye from Jupyter")
```
![](/images/websuite_jupyter_code.png)

Click the play button to run the cell, and wait for the result.

Assuming everything has been configured correctly, it will run without issues.
+++