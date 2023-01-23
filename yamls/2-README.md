## kubernetes jobs and cron jobs


# Jobs
A Job creates one or more Pods and will continue to retry execution of the Pods until a specified number of them successfully terminate



## Running an example Job
Here is an example Job config.

1-job.yaml

```
kubectl apply -f 2-job.yaml
kubectl get all
kubectl logs <pod-name>
kubectl describe job hello-job
kubectl delete job hello-job
```

## killing pods
```
kubectl apply -f 2-job-to-kill.yaml
kubectl get all
kubectl delete pod <job-pod-name>
```

job completion


## restarts  pods


https://kubernetes.io/docs/concepts/workloads/controllers/job/
