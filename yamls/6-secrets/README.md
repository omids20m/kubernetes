`
DB_Host: DatabaseHost
DB_User: user1
DB_Password: P@ssw0rd
`

## Secrets
```
kubectl get secret --help
kubectl create secret --help
kubectl create secret generic --help
```

## Creating secret
```
#kubectl create secret generic secret-demo1 --from-literal=username=omid --from-literal=password=P@ssw0rd
#kubectl create secret generic secret-demo2 --from-literal=username=omid --from-file=path/to/file.txt
kubectl get secret
kubectl describe secret
kubectl describe secret -o yaml
```

```
kubectl apply -f 1-app-secret.yaml
```

## Encoding secret values 
`
echo -n 'DatabaseHost' | base64
RGF0YWJhc2VIb3N0
echo -n 'RGF0YWJhc2VIb3N0' | base64 --decode

echo -n 'user1' | base64
XNlcjE=
echo -n 'XNlcjE=' | base64 --decode

echo -n 'P@ssw0rd' | base64
UEBzc3cwcmQ=
echo -n 'UEBzc3cwcmQ=' | base64 --decode
`
kubectl apply -f 1-app-secret.yaml

kubectl get secret
kubectl describe secrets

kubectl get secret app-secret -o yaml

## Secret in pods