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
- Launch a pod (this will create an ubuntu VM that sleeps for 10 minutes then exits)
```shell
kubectl apply -f test.yaml
```
- Check that the pod is running
```shell
kubectl get pods -o wide
```

- The pod should be running without issues.

## Perform Network Test


- Create yaml file for a php-apache service
```shell
curl -L https://k8s.io/examples/application/php-apache.yaml > php-apache.yaml
```
- Launch pod service
```shell
kubectl apply -f php-apache.yaml
```
- Create yaml file for VM to verify connection from
```shell
cat << EOF > busybox-wget.yaml
apiVersion: v1
kind: Pod
metadata:
  name: busybox-wget
  labels:
    app: busybox-wget
spec:
  containers:
  - image: busybox:1.28.4
    command:
      - "wget"
      - "-q"
      - "-O-"
      - "http://php-apache"
    imagePullPolicy: IfNotPresent
    name: busybox-wget
  restartPolicy: Never
EOF
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