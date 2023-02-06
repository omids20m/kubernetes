# Init Container

if any of init container fails, the pod will get restarted
if you dont want to do that you can set restartPolicy=Never and the pod will never restarted 

## example
1. Creating a volume shared between initContainer that creating an index.html file in the shared volume and exits
2. The the actual Container (Nginx container) mounts the shared volume and index.html

```
watch kubectl get all -o wide
kubectl apply -f 1-deployment.yaml
kubectl describe deploy nginx-deployment
```

```
watch kubectl get all -o wide
##kubectl expose deploy nginx-deployment --type NodePort --port 80
kubectl apply -f 2-service.yaml
```

browse http://kworker1:32321

## Scale deployment 
```
watch kubectl get all -o wide
kubectl scale deploy nginx-deploy --replicas=2
```
## Multiple init containers
you can have multiple initContainers
init containers runs sequentially

```
delete -f 1-deployment.yaml
delete -f 2-service.yaml
```

## make init container fail
change command to raise an error

watch kubectl get all -o wide

it will restart the initContainer 
and keeps on restarting untill all initContainers succeeded 

kubectl describe deploy nginx-deployment

State
  Reason: CrashLoopBackoff
  Message: ........
  ...
  ...
  Restart Count: 3

```
delete ...
```