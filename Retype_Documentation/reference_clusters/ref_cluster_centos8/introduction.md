---
order: 100
label: Introduction
icon: dot
---

This documentation will describe the process of setting up a cluster with all the capabilities shown in the other parts of the documentation. This will not explain the process, only list the necessary steps.

This is also **not** a guide, simply an example of an installation process that may be of use to those setting up a cluster. Several things are specific to this cluster:

- The cluster has 3 nodes.
- Every node on the cluster has an operating system installed, specifically [Centos 8](https://www.centos.org/download/#centos-stream).
- Every node is on the network 10.50.0.0
- The nodes described are instances created with OpenStack and can connect to upstream repositories.


![A diagram of the cluster used.](/images/cluster_diagram.png)


## Testing

On each page there is a Testing section with instructions on how to check if everything was set up correctly. The testing assumes that all previous instructions were completed without issues. 

!!!
The testing can help find where an issue may have happened, but it does not provide solutions for fixing issues.
!!!


