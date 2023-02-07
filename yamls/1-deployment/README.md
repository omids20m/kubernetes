<<<<<<< HEAD
Play with kubernetes pods / replicaset / deployment

## Deploy a single pod
=======
>>>>>>> d97ee8a138d57ee845b0041f99127a48e7476d9e
```
username: omid
password: P@ssw0rd
```

## Secrets
```
kubectl get secret --help
kubectl create secret --help
kubectl create secret generic --help
```


## Encoding secret values 
```
echo -n 'omid' | base64
b21pZA==
echo -n 'b21pZA==' | base64 --decode

echo -n 'P@ssw0rd' | base64
UEBzc3cwcmQ=
echo -n 'UEBzc3cwcmQ=' | base64 --decode

kubectl apply -f 1-secret-demo.yaml

kubectl get secret
kubectl describe secrets

```

## Creating secret
```
#kubectl create secret generic secret-demo1 --from-literal=username=omid --from-literal=password=P@ssw0rd
#kubectl create secret generic secret-demo2 --from-literal=name=omid --from-file=secret-file.txt

kubectl apply -f 1-secret-demo.yaml
kubectl apply -f 2-deployment-secret-env.yaml

kubectl get secret
kubectl describe secret
```

```
kubectl exec -it secret-demo-deploy-<podname> [-c <Container Name>] -- sh
# kubectl exec -it secret-demo-deploy-b6b95b9-k4m2q -- sh 
env | grep username
echo $username
```

<<<<<<< HEAD
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


=======
## Updating secrets
