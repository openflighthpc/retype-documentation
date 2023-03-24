---
order: 70
label: Using a Job Script
icon: dot-fill
---

To use a job script, select "Browse scripts" from the management page. If the user currently has no created job scripts, they will be given the option to go to [Create a Job Script](/hpc_environment_usage/slurm_environment_usage/flight_job/flight_job_manager/creating_a_job_script/). 

If the user already has at least one job script, they are shown all of their job scripts. 

![](/images/flight_web_jobmanager_submit.png)

By clicking on a job script, the user can view it, submit it to be run, and delete it.

![](/images/flight_web_jobmanager_selected.png)

### Viewing a Job Script

To view a script, click on it, then click "View script".

![](/images/flight_web_jobmanager_submit_view.png)

While viewing a script, the user can:
- View the contents of the script in the code block on the left.
- Edit the script notes on the right by pressing the "edit" button near the notes. 
- Edit the script itself by pressing the "edit" button above the script text.
- [Submit the job script](/hpc_environment_usage/slurm_environment_usage/flight_job/flight_job_manager/using_a_job_script/#submitting-a-job-script)
- [Delete the job script](/hpc_environment_usage/slurm_environment_usage/flight_job/flight_job_manager/using_a_job_script/#deleting-a-job-script)

### Submitting a Job Script

To submit a script, click on the ":icon-rocket: Submit" button. After doing so the user will be asked a series of questions about the details of the job.

![](/images/flight_web_jobmanager_submit_submit.png)

When all the questions are completed, a summary of the job details is displayed. 
![](/images/flight_web_jobmanager_submit_finish.png)

At this point, the ":icon-rocket: Submit" button will have the job start running on the cluster. The user will be taken to a page with an overview of the job. 

![](/images/flight_web_jobmanager_submit_running.png)

Here the job can be cancelled, and when it is complete the output can be viewed by clicking the files that appear in the "Results directory" section.

### Deleting a Job Script

Press the "Delete" button to delete the job script. A window will ask the user to confirm, after which it will be deleted.

