Creating and exploring an nginx deployment 
==========================================

This YAML file describes a Deployment that runs the nginx:1.14.2 Docker image:

1. Create a Deployment based on the YAML file:
```
kubectl apply -f deployment.yaml -n demo
```

The output is similar to this:
> deployment.apps/nginx-deployment created


2. Display information about the Deployment:
```
kubectl describe deployment nginx-deployment -n demo
```
The output is similar to this:
>
    Name:                   nginx-deployment
    Namespace:              demo
    CreationTimestamp:      Wed, 16 Feb 2022 18:29:06 +0330
    Labels:                 <none>
    Annotations:            deployment.kubernetes.io/revision: 1
    Selector:               app=nginx
    Replicas:               2 desired | 2 updated | 2 total | 2 available | 0 unavailable
    StrategyType:           RollingUpdate
    MinReadySeconds:        0
    RollingUpdateStrategy:  25% max unavailable, 25% max surge
    Pod Template:
    Labels:  app=nginx
    Containers:
    nginx:
        Image:        nginx:1.14.2
        Port:         80/TCP
        Host Port:    0/TCP
        Environment:  <none>
        Mounts:       <none>
    Volumes:        <none>
    Conditions:
    Type           Status  Reason
    ----           ------  ------
    Available      True    MinimumReplicasAvailable
    Progressing    True    NewReplicaSetAvailable
    OldReplicaSets:  <none>
    NewReplicaSet:   nginx-deployment-9456bbbf9 (2/2 replicas created)
    Events:
    Type    Reason             Age   From                   Message
    ----    ------             ----  ----                   -------
    Normal  ScalingReplicaSet  14s   deployment-controller  Scaled up replica set nginx-deployment-9456bbbf9 to 2


1. List the Pods created by the deployment:
```
kubectl get pods -l app=nginx -n demo
```
The output is similar to this:
>
    NAME                               READY   STATUS    RESTARTS   AGE
    nginx-deployment-9456bbbf9-2t4xk   1/1     Running   0          55s
    nginx-deployment-9456bbbf9-fmqg2   1/1     Running   0          55s

1. Display information about a Pod:
```
kubectl describe pod nginx-deployment-9456bbbf9-fmqg2 -n demo
```
where `nginx-deployment-9456bbbf9-fmqg2` is the name of one of your Pods.

Creating a Service 
==================
1. Firstway: using kubectl command
```
kubectl expose deployment/nginx-deployment --type=NodePort -n demo
```

The output is similar to this:
> service/nginx-deployment exposed

2. or Secondway: using yaml file
```
kubectl apply -f service.yaml -n demo
```
The output is similar to this:
> service/nginx-service created

```
kubectl get all -n demo
```

The output is similar to this:
> 
    NAME                                   READY   STATUS    RESTARTS   AGE
    pod/nginx-deployment-9456bbbf9-2t4xk   1/1     Running   0          7m34s
    pod/nginx-deployment-9456bbbf9-fmqg2   1/1     Running   0          7m34s

    NAME                    TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
    service/nginx-service   NodePort   10.233.56.169   <none>        80:30386/TCP   32s

    NAME                               READY   UP-TO-DATE   AVAILABLE   AGE
    deployment.apps/nginx-deployment   2/2     2            2           7m34s

    NAME                                         DESIRED   CURRENT   READY   AGE
    replicaset.apps/nginx-deployment-9456bbbf9   2         2         2       7m34s

browse http://10.237.208.133:30386
where `10.237.208.133` is ip address of one of your worker nodes


Updating the deployment 
=======================

1. Apply the new YAML file:
```
kubectl apply -f deployment-update.yaml -n demo
```

2. Watch the deployment create pods with new names and delete the old pods:
```
kubectl get pods -l app=nginx -n demo
```

browse http://10.237.208.133:30386
where `10.237.208.133` is ip address of one of your worker nodes


Scaling the application by increasing the replica count 
=======================================================
You can increase the number of Pods in your Deployment by applying a new YAML file. This YAML file sets replicas to 4, which specifies that the Deployment should have four Pods:

1. Apply the new YAML file:
```
kubectl apply -f deployment-scale.yaml -n demo
```

2. Verify that the Deployment has four Pods:
```
kubectl get pods -l app=nginx -n demo
```
The output is similar to this:
>

Deleting a deployment
=====================
Delete the deployment by name:
```
kubectl delete deployment nginx-deployment -n demo
```



