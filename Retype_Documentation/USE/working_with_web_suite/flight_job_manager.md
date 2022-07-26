---
order: 70
label: Flight Job Manager
icon:
---

## Logging In

After selecting the file manager service, a page with the description and a login box will be presented. The same user details used for accessing the cluster from a CLI are used to authenticate the session.

![](/images/flight_web_jobmanager_login.png)

![](/images/flight_web_login.png)

On successful login, the job manager will be ready to be used.

![](/images/flight_web_jobmanager_options.png)


## Creating a Job Script

To create a job script, select "Browse script templates" from the management page. There are instructions at the top of the page, but job script creation shall be described here as well.

![](/images/flight_web_jobmanager_creation.png)

- Select one of the templates from those listed. Each template has a description of what it should be used for.
- Click "Create Script".
- The user will be asked a series of questions which will modify the script to suit them specifically. These include the preferred working directory, output file name, and more.

![](/images/flight_web_jobmanager_creation_question.png)

!!!
Each question comes with an explanation, but if uncertain, there is always a default answer.
!!!

## Submitting a Job Script

To submit a job script, select "Browse scripts" from the management page. If the user currently has no created job scripts, they will be given the option to go to [Create a Job Script](/USE/working_with_web_suite/flight_job_manager/#creating-a-job-script). 

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
- [Submit the job script](/USE/working_with_web_suite/flight_job_manager/#submitting-a-job-script-1)
- [Delete the job script](/USE/working_with_web_suite/flight_job_manager/#deleting-a-job-script)

### Submitting a Job Script

To submit a script, click on the ":icon-rocket: Submit" button. After doing so the user will be asked a series of questions about the details of the job.

![](/images/flight_web_jobmanager_submit_submit.png)

When all the questions are completed, a summary of the job details is displayed. 
![](/images/flight_web_jobmanager_submit_finish.png)

At this point, the ":icon-rocket: Submit" button will have the job start running on the cluster. The user will be taken to a page with an overview of the job. 

![](/images/flight_web_jobmanager_submit_running.png)

Here the job can be cancelled, and when it is complete the output can be viewed by clicking the files that appear in the "Results directory" section.

### Deleting a Job Script



## Monitoring a Job

To monitor a job, select "Monitor jobs" from the management page.