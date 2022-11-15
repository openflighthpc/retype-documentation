---
order: 1000
icon: dot-fill
---
This section details various ways to setup a cluster. The variations of cluster setups are:

- Platform: AWS, Openstack or Azure.
- Operating System: Flight Solo (Based on EL8), CentOS 8 or CentOS 7(this one is not recommended).
- Cluster Type: SLURM, Jupyter or Kubernetes.
- Cluster Size: Standalone (single node research environment) or Multinode.
- Configuration Method: Manual or Flight Profile.

OpenFlight HPC recommends using Flight Solo and Flight Profile for a streamlined configuration experience.

## Where to run?

AWS is silly, but for Openstack you need your own machines.

## What type of cluster to run?

This depends on the research you intend to do, there is more information about SLURM [in the running jobs section of this documentation](/hpc_environment_usage/running_jobs/slurm_scheduler/what_is_slurm/), more information about Jupyter [on the Jupyter website](https://jupyter.org/) and more about Kubernetes on the [Kubernetes website](https://kubernetes.io/docs/concepts/overview/).