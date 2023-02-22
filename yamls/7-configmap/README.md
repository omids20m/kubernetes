
You can set vales in docker file but every time that values need to be changed, you should re-deploy docker image.


## Creating ConfigMaps from yaml file
```
kubectl get configmaps --help
kubectl get cm --help
kubectl apply -f 1-configmap.yaml
kubectl describe configmap demo-configmap
kubectl describe configmap demo-configmap -o yaml
```


## Creating ConfigMaps cli
```
kubectl create configmap demo-configmap-1 --from-literal=person.name=Omid --from-literal=person.lastname=Shariati
kubectl get configmap
kubectl describe configmap demo-configmap-1
```

```
kubectl create configmap demo-configmap-1 --from-file=
```

# Using configmap inside a container
```
kubectl get pods
kubectl apply -f 2-pod-configmap-env.yaml
kubectl get pods
kubectl exec -it busybox sh
```

```
echo $NAME
echo $LASTNAME 
env | grep -i NAME
```

```
kubectl delete pod busybox 
```

# Mount configmap as a volume inside container
```
3-pod-configmap-volume.yaml
kubectl apply -f 3-pod-configmap-volume.yaml
kubectl get pods
kubectl exec -it busibox sh
```

```
env | grep -i NAME
ls /mydata
cat /mydata/person.Name
cat /mydata/person.LastName
```

# When the changes happens?
```
kubectl edit cm demo-configmap

# edit some values here

kubectl get cm demo-configmap -o yaml
kubectl get pod
kubectl exet -it busybox sh

cat /mydata/person.Name
cat /mydata/person.Name
cat /mydata/person.Name
cat /mydata/person.Name
```

times to apply configmap chnges depends on cluster load, scheduler decide to apply it

kubectl delete pod busybox
kubectl delete cm demo-configmap


# Using a file for creating configmap
```
kubectl create configmap mysql-demo-config --from-file=mysql-config.cnf

kubectl get cm 
kubectl get cm mysql-demo-config -o yaml

kubectl delete cm mysql-demo-config

# How to use this configmap inside a pod? (as env & as a volume)

```

# Using a configmap with inline file content
```
kubectl apply -f 5-configmap-inline-file.yaml
kubectl apply -f 4-pod-configmap-mysql-volume.yaml

kubectl get cm mysql-demo-config -o yaml 
kubectl get pods

kubectl delete pods busybox
kubectl describe pods busybox
kubectl apply -f 4-pod-configmap-mysql-volume.yaml


kubectl get pods
kubectl exec -it busybox sh

ls /mydata
cat /mydata/mysql-config.cnf
```

## updating the configmap
```
vi 5-configmap-inline-file.yaml

kubectl apply -f 5-configmap-inline-file.yaml
kubectl get cm mysql-demo -o yaml

kubectl exec -it busybox sh 

ls /mydata/
cat /mydata/.....

kubectl get all
```


