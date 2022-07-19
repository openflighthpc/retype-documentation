---
order: 70
label: Why use a job-scheduler on a personal research environment?
---

Good question. On shared multi-user research environments, a job-scheduler is often used as a control mechanism to make sure that users don’t unfairly monopolise the valuable compute resources. In extreme cases, the scheduler may be wielded by system administrators to force “good behaviour” in a shared environment, and can feel like an imposition to research environment users.

With your own personal research environment, you have the ability to directly control the resources available for your job - you don’t need a job-scheduler to limit your usage.

However - there are a number of reasons why your own job-scheduler can still be a useful tool in your research environment:

1. It can help you organise multi-stage work flows, with batch jobs launching subsequent jobs in a defined process.
2. It can automate launching of MPI jobs, finding available nodes to run applications on.
3. It can help prevent accidentally over-allocating CPUs or memory, which could lead to nodes failing.
4. It can help bring discipline to the environment, providing a consistent method to replicate the running of jobs in different environments.
5. Jobs queued in the scheduler can be used to trigger scaling-up the size of your research environment, with compute nodes released from the research environment when there are no jobs to run, saving you money.

Your OpenFlight Flight Compute research environment comes with a job-scheduler pre-installed, ready for you to start using. The scheduler uses very few resources when idle, so you can choose to use it if you find it useful, or run jobs manually across your research environment if you prefer.


