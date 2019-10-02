Jobs are used to run a specific task and complete it successfully by
creating the POD at that point of time and status changes to "Completed"

CronJobs are designed to run a task at specific point of time scheduled.

Entries for CronJobs to run on specific time:
Minute (0-59)
Hour (0-23)
Day of the Month (1-31)
Month (1-12)
Day of the week (0-6) starting from Sunday

How to suspend the job?
kubectl patch cronjobs <job-name> -p '{"spec" : {"suspend" : false}}'

