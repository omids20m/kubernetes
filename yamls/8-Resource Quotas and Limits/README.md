# Using Resource Quotas & Limits in Kubernetes Cluster

cpu ram disk by namespaces

## Using quota to limit number of resources
```
kubectl create namespace quota-demo-ns
kubectl get ns
kubectl get nodes

# Resource quotas
## the quantity of the resources you can deploy on your cluster
kubectl apply -f 1-quota-count.yaml
kubectl describe quota quota-demo1 -n quota-demo-ns 

kubectl create cm cm1 --from-literal=key1=value1 -n quota-demo-ns

kubectl get cm -n quota-demo-ns 
kubectl describe quota quota-demo1 -n quota-demo-ns 


kubectl create cm cm2 --from-literal=key2=value2 -n quota-demo-ns
```
output:
```
Error from server (Forbidden): configmap "cm2" is forbidden: exceeded quota: quota-demo1,configmap=1
```

```
kubectl describe quota-demo1 -n quota-demo-ns
kubectl get all -n quota-demo-ns

kubectl apply -f 2-nginx-deploy.yaml -n quota-demo-ns
kubectl scale deploy nginx-deploy --replicas=2 -n quota-demo-ns

kubectl describe quota-demo1 -n quota-demo-ns


kubectl scale deploy nginx-deploy --replicas=3 -n quota-demo-ns

kubectl get all -n quota-demo-ns
# Ready 2/3 Desired 3 Current 2

kubectl describe replicaset <nginx-replica123> -n quota-demo-ns

# delete all resources

kubectl delete deploy nginx-deploy -n quota-demo-ns
kubectl delete quota quota-demo1 -n quota-demo-ns

kubectl get all -n quota-demo-ns

```


## Using quota to limit number of resources
## Resource limits (cpu / memory / storage)
```
kubectl apply -f 3-quota-mem.yaml -n quota-demo-ns

kubectl describe quota quota-demo-mem -n quota-demo-ns
```

```
kubectl apply -f 4-pod-quota-mem.yaml -n quota-demo-ns
# it fails

# add resource limits
vi 4-pod-quota-mem.yaml

kubectl apply -f 4-pod-quota-mem.yaml -n quota-demo-ns

kubectl describe quota-demo-mem -n quota-demo-ns
```

## set memory limits of pod above the quota limit
```
vi 4-pod-quota-mem.yaml
# set memory limit to 800Mi

kubectl apply -f 4-pod-quota-mem.yaml -n quota-demo-ns

kubectl describe quota-demo-mem -n quota-demo-ns
```
output:
```
Error from server (Forbidden): error creating ".....": pods "nginx"    : limits.memory:800Mi, used: limits.memory=0, limited: limits.memory=500Mi
```


## Using default LimitRange for limiting pod resources
```
vi 4-pod-quota-mem.yaml
# delete resources and limits
kubectl apply -f 4-pod-quota-mem.yaml -n quota-demo-ns
# Error

kubectl apply -f 5-quota-limitrange.yaml
kubectl describe limitrange mem-limitrange -n quota-demo-ns

kubectl apply -f 4-pod-quota-mem.yaml -n quota-demo-ns


kubectl delete -f 4-pod-quota-mem.yaml -n quota-demo-ns
# delete all
```

## limits.memory and request.memory 
limits.memory: all the pods can use more than this value
requestrequest.memory: is the maximum memory that pod can request

```
kubectl apply -f 6-quota-mem.yaml -n quota-demo-ns
vi 6-pod-quota-mem.yaml
# remove requests
kubectl apply -f 6-pod-quota-mem.yaml -n quota-demo-ns
# Error ... (Forbidden)
# note when request.memory is not set, it will be same as limits.memory

vi 6-pod-quota-mem.yaml
# adding requests. memory

kubectl apply -f 6-pod-quota-mem.yaml -n quota-demo-ns
kubectl describe pod nginx -n quota-demo-ns
# ...

kubectl delete -f 6-pod-quota-mem.yaml -n quota-demo-ns
vi 6-pod-quota-mem.yaml
# set requests.memory to 150Mi

kubectl describe quota quota-demo1 -n quota-demo-ns 
# max is 100 but we set 200
```
