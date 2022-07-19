---
order: 100
label: Shared filesystem
---

Your OpenFlight Compute research environment includes a shared home filesystem which is mounted across the login and all compute nodes. Files copied to this area are available via the same absolute path on all research environment nodes. The shared filesystem is typically used for job-scripts, input and output data for the jobs you run.

!!!
If running a single node research environment then the home directory is not shared over NFS as there are no other resources to share data with.
!!!