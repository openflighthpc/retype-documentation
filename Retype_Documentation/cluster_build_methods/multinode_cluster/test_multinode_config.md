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

- As the `default_username` check nodes are "Ready" 
    ```shell
	kubectl get nodes
	```

## Launching a "Pod"

- Create test yaml file for the VM 
```shell
cat << EOF > test.yaml
apiVersion: v1
kind: Pod
metadata:
  name: ubuntu
  labels:
    app: ubuntu
spec:
  containers:
  - image: ubuntu
    command:
      - "sleep"
      - "600"
    imagePullPolicy: IfNotPresent
    name: ubuntu
  restartPolicy: Never
EOF
```
- Launch pod (this will create an ubuntu VM that sleeps for 10 minutes then exits)
```shell
kubectl apply -f test.yaml
```
- Check pod running
```shell
kubectl get pods -o wide
```
+++