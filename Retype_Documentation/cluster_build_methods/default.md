---
order: 50
label: Cluster Build Methods
icon: versions

---
This section details various ways to setup a cluster. The variations of cluster setups are:

- Platform: AWS, Openstack or Azure[^1].
- Operating System: Flight Solo (Based on EL8), CentOS 8 or CentOS 7(this one is not recommended).
- Cluster Type: SLURM, Jupyter[^1] or Kubernetes[^1].
- Cluster Size: Standalone (single node research environment) or Multinode.
- Configuration Method: Manual or Flight Profile.

OpenFlight HPC recommends using Flight Solo and Flight Profile for a streamlined configuration experience.

## Where to run?

Amazon Web Services, Openstack and Microsoft Azure are all tried and tested cloud platforms that support OpenflightHPC. Any cloud computing platforms not mentioned in this documentation would likely work, but figuring that out will be up to you.

## What type of cluster to run?

This depends on the research you intend to do, there is more information about SLURM [in the running jobs section of this documentation](/hpc_environment_usage/running_jobs/slurm_scheduler/what_is_slurm/), more information about Jupyter [on the Jupyter website](https://jupyter.org/) and more about Kubernetes on the [Kubernetes website](https://kubernetes.io/docs/concepts/overview/).

## How to configure a cluster?

Generally, two ways to configure a cluster are offered: with Flight Profile, or manually. Flight Profile is a tool that simplifies multinode and standalone cluster configurations, **and OpenflightHPC highly recommends using it**. However, some people prefer to make their own way, and for those there are instructions on manually configuring a cluster. 

## What size of cluster?


There are two possible sizes: standalone and multinode. Standalone is just a single node, but depending on what it is hosted by it may be quite powerful. Multinode is a more traditional cluster, as it is made up of multiple instances joined together.

[^1]: Coming soon.