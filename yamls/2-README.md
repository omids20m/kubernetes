## kubernetes jobs and cron jobs


# Jobs

A Job creates one or more Pods and will continue to retry execution of the Pods until a specified number of them successfully terminate



## Running an example Job

Here is an example Job config. It computes π to 2000 places and prints it out. It takes around 10s to complete.

1-job.yaml



https://kubernetes.io/docs/concepts/workloads/controllers/job/
