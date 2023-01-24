
## Deploy a single pod
```
kubectl apply -f 1-nginx-pod.yaml
kubectl get pods -o wide
kubectl get events
kubectl describe pod nginx
kubectl delete -f 1-nginx-pod.yaml
#kubectl delete pod <pod-name>
```

## Deploy a replicaset
```
kubectl apply -f 1-nginx-replicaset.yaml
kubectl get replicaset -o wide
kubectl get events

kubectl describe pod nginx
kubectl delete -f 1-nginx-replicaset.yaml
```


kubectl exec -it nginx -- sh




