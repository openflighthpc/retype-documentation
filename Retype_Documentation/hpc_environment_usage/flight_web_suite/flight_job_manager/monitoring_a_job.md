---
order: 60
label: Monitoring a Job
icon: dot-fill
---

To monitor a job, select "Monitor jobs" from the management page. This page displays all the jobs that either have run or are running.

![](/images/flight_web_jobmanager_monitor.png)

### More information
The user can see more information by clicking on a job. This information changes based on the status of the job. Regardless of status, basic information about the job such as ID, time since submission or time to completion is always displayed. 


#### Job Status: Running

The "Running" status allows the user to cancel the job, but since the job has not yet finished there are no results.

![](/images/flight_web_jobmanager_monitor_select_running.png)

#### Job Status: Cancelled

The "Cancelled" status results from the user cancelling a job, the time since cancellation is displayed instead of time to completion. Since the job was cancelled before it could be completed, there is no results output.

![](/images/flight_web_jobmanager_monitor_select_cancelled.png)

#### Job Status: Completed

The "Completed" status results from the job running to completion. The "Results directory" allows the user to view the output file.

![](/images/flight_web_jobmanager_monitor_select_completed.png)

#### Job Status: Failed

The "Failed" status results from an issue with the job. In the example below more memory was requested than was available to the cluster. A job could also fail from requesting too many nodes, too many CPUs, or running out of time.

![](/images/flight_web_jobmanager_monitor_select_failed.png)

If a job has been cancelled, completed or failed, then it can be removed from the job list with the red "Remove" button.
