---
order: 40
label: '4\. Testing a Multinode Cluster configuration'
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

2. Run the script with `sbatch simplejobscript.sh`, and to test all your nodes try queuing up enough jobs that all nodes will have to run.

3. The job(s) should start and complete without issues.
+++ Kubernetes

## Check Nodes Running/Ready

- As the `default_username` (unless this was changed, it will be `flight`) check nodes are "Ready" 
    ```shell
    kubectl get nodes
    ```
## Launching a "Pod"

- Get test yaml file for the VM 
    ```
    flight silo file pull openflight:kubernetes/pod-launch-test.yaml
    ```

- Launch a pod (this will create an ubuntu VM that sleeps for 10 minutes then exits)
    ```shell
    kubectl apply -f pod-launch-test.yaml
    ```
- Check that the pod is running
    ```shell
    kubectl get pods -o wide
    ```

- The pod should be running without issues.

## Perform Network Test


- Create yaml file for a php-apache service
    ```shell
    flight silo file pull openflight:kubernetes/php-apache.yaml
    ```
- Launch pod service
    ```shell
    kubectl apply -f php-apache.yaml
    ```
- Get yaml file for VM to verify connection from
    ```shell
    flight silo file pull openflight:kubernetes/busybox-wget.yaml
    ```
- Launch pod
    ```shell
    kubectl apply -f busybox-wget.yaml
    ```
- View output of wget pod (this should show `OK!`)
    ```shell
    kubectl logs busybox-wget
    ```
+++