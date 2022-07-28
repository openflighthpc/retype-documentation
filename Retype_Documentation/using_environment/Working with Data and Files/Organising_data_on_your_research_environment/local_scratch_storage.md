---
order: 80
label: Local scratch storage
icon: dot-fill
---

Your compute nodes have an amount of disk space available to store temporary data under the `/tmp` mount-point. This area is intended for temporary data created during compute jobs, and shouldn’t be used for long-term data storage. Compute nodes are configured to clear up temporary space automatically, removing orphan data left behind by jobs.

Users must make sure that they copy data they want to keep back to the shared filesystem after compute jobs have been completed.