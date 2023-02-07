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
env | grep username
echo $username
```

## Secret in pods