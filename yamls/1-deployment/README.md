<<<<<<< HEAD:yamls/README.md

Play with kubernetes pods / replicaset / deployment

## Deploy a single pod
```
kubectl apply -f 1-nginx-pod.yaml
kubectl get pods
kubectl get pods -o wide
kubectl get events
kubectl describe pod nginx
kubectl delete -f 1-nginx-pod.yaml
#kubectl delete pod <pod-name>
```

## Deploy a replicaset
```
kubectl apply -f 1-nginx-replicaset.yaml
kubectl get replicaset
kubectl get all
kubectl delete pod <one-of-pod-names>
kubectl get all
kubectl delete -f 1-nginx-replicaset.yaml
```

```
kubectl apply -f 1-nginx-deployment.yaml
kubectl get deployment
kubectl get all
kubectl describe pod <one-of-pod-names>
kubectl get replicaset
kubectl describe replicaset <replicaset-name>
kubectl delete -f 1-nginx-replicaset.yaml
```

## how to find out the list of pods with the lable of app=nginx-web
```
kubectl get pods -l app=nginx-web
```

## scale
```
kubectl scale deploy nginx-deploy --replicas=3
```

## namespaces
kubectl get pods -n kube-system

kubectl get pods
kubectl get pods <pod-name> -o yaml
kubectl get pods <pod-name> -o yaml > /tmp/my-pod.yamp

kubectl exec -it nginx -- sh



=======

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




>>>>>>> 3571823ccae22dce0c25709cacfc5b543cf9dd91:yamls/1-deployment/README.md
