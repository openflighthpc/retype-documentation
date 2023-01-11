---
order: 40
label: '4\. Testing a Multinode Cluster configuration'
icon: dot
---

After the creation and configuration of nodes has been complete, everything should work. Here are several tests to confirm this.

+++ Slurm

```
sbatch testscript
```
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
+++ Jupyter


python says "hiss"
+++