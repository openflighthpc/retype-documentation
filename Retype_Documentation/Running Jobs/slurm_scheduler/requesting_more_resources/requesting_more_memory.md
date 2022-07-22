---
order: 80
label: Requesting more memory
icon: dot
---

In order to promote best use of the research environment scheduler - particularly in a shared environment, it is recommended to inform the scheduler the maximum required memory per submitted job. This helps the scheduler appropriately place jobs on the available nodes in the research environment.

You can specify the maximum amount of memory required per submitted job with the `--mem=<MB>` option. This informs the scheduler of the memory required for the submitted job. Optionally - you can also request an amount of memory _per CPU core_ rather than a total amount of memory required per job. To specify an amount of memory to allocate _per core_, use the `--mem-per-cpu=<MB>` option.

Examples:

`--mem=200` - Requesting 200MB of memory.

`--mem-per-cpu=10` - Requesting 10MB of memory per CPU.
!!!
When running a job across multiple compute hosts, the `--mem=<MB>` option informs the scheduler of the required memory per node
!!!
