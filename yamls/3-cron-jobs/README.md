# kubernetes cron jobs

## Cron expression

```
# ┌───────────── minute (0 - 59)
# │ ┌───────────── hour (0 - 23)
# │ │ ┌───────────── day of the month (1 - 31)
# │ │ │ ┌───────────── month (1 - 12)
# │ │ │ │ ┌───────────── day of the week (0 - 6) (Sunday to Saturday;
# │ │ │ │ │                                   7 is also Sunday on some systems)
# │ │ │ │ │
# │ │ │ │ │
# * * * * * <command to execute>
```

    , @weekly, @monthly

https://en.wikipedia.org/wiki/Cron

## creating cronjob

## Deleteing jobs issues

```
kubectl delete cronjob <--->
```

when delete a job it mightly some of the jobs and pods works in background
kubectl delete pods --all

## Retention

## successfulJobsHistoryLimit & failedJobsHistoryLimit

by default retain the last 3 successful jobs and last 1 failed job.
pods

```
successfulJobsHistoryLimit: 3
failedJobsHistoryLimit: 1
```

## suspending and resuming cron jobs (kubectl apply, patch)

prevents the cronjobs from any new scheduling jobs/pods

```
spec:
  suspend: true
```

```
kubectl get all
kubectl describe cronjob hello-cronjob
```

resuming cronjob

```
kubectl patch cronjob hello-cron -p '{"spec":{"suspend":false}}'
kubectl get all
kubectl delete cronjob hello-cronjob
```

# concurrencyPolicy

```
spec:
  concurrencyPolicy: Allow Forbid Replace
```

there is a job running, what should I do?
