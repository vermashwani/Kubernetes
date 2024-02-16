# Kubernetes
## 1. DaemonSet
Containts will go here....

## 2. Kube-proxy
Containts will go here....



## 3. Kubelet
Containts will go here....



## 3. Taints and Tolerations
Containts will go here....


## 4. Node
+ ### NodeSelector
```
[node1 ~]$ kubectl get nodes
NAME    STATUS   ROLES           AGE   VERSION
node1   Ready    control-plane   40m   v1.27.2
node2   Ready    <none>          38m   v1.27.2
node3   Ready    <none>          35m   v1.27.2
```


```
[node1 ~]$ kubectl get node --show-labels
```
```
NAME    STATUS   ROLES           AGE     VERSION   LABELS
node1   Ready    control-plane   6m44s   v1.27.2   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=node1,kubernetes.io/os=linux,node-role.kubernetes.io/control-plane=,node.kubernetes.io/exclude-from-external-load-balancers=
node2   Ready    <none>          4m46s   v1.27.2   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=node2,kubernetes.io/os=linux
node3   Ready    <none>          116s    v1.27.2   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=node3,kubernetes.io/os=linux
```
#### Add labels on all nodes
<pre>
[node1 ~]$ kubectl label nodes node1 <b>capacity=medium</b>
node/node1 labeled
[node1 ~]$ kubectl label nodes node2 <b>capacity=low</b>
node/node2 labeled
[node1 ~]$ kubectl label nodes node3 <b>capacity=high</b>
node/node3 labeled
</pre>

#### Verify node labels
<pre>[node1 ~]$ kubectl get node <b>--show-labels</b></pre>

<pre>
NAME    STATUS   ROLES           AGE     VERSION   LABELS
node1   Ready    control-plane   9m41s   v1.27.2   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,<b>capacity=medium</b>,kubernetes.io/arch=amd64,kubernetes.io/hostname=node1,kubernetes.io/os=linux,node-role.kubernetes.io/control-plane=,node.kubernetes.io/exclude-from-external-load-balancers=
node2   Ready    <none>          7m43s   v1.27.2   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,<b>capacity=low</b>,kubernetes.io/arch=amd64,kubernetes.io/hostname=node2,kubernetes.io/os=linux
node3   Ready    <none>          4m53s   v1.27.2   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,<b>capacity=high</b>,kubernetes.io/arch=amd64,kubernetes.io/hostname=node3,kubernetes.io/os=linux
</pre>

<pre>
[node1 ~]$ <b>kubectl run nginx --image=nginx:latest --restart=Never --dry-run -o yaml > pod.yaml</b>
W0215 17:33:47.730888    4304 helpers.go:692] --dry-run is deprecated and can be replaced with --dry-run=client.
</pre>
#### Install vim to modify the code easily
```
[node1 ~]$ yum install vim -y
```
#### Open **pod.yaml** and add highlighted text
```
[node1 ~]$ vim pod.yaml 
```
<pre>
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx
spec:
  <b>nodeSelector:
    capacity: low</b>
  containers:
  - image: nginx:latest
    name: nginx
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}
</pre>
#### Verify your yaml file changes
```
[node1 ~]$ cat pod.yaml 
```
``` yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx
spec:
  nodeSelector:
    capacity: low
  containers:
  - image: nginx:latest
    name: nginx
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}
```
#### Deploy a pod
```
[node1 ~]$ kubectl apply -f pod.yaml 
pod/nginx created
```
#### Verify pod should be created on **capacity=low** labeled node
<pre>
[node1 ~]$ kubectl get pod -o wide
NAME    READY   STATUS    RESTARTS   AGE   IP         NODE    NOMINATED NODE   READINESS GATES
nginx   1/1     Running   0          14m   10.5.1.5   <b>node2</b>   <none>           <none>
</pre>
<pre>
[node1 ~]$ kubectl get node --show-labels
NAME    STATUS   ROLES           AGE   VERSION   LABELS
node1   Ready    control-plane   34m   v1.27.2   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,capacity=medium,kubernetes.io/arch=amd64,kubernetes.io/hostname=node1,kubernetes.io/os=linux,node-role.kubernetes.io/control-plane=,node.kubernetes.io/exclude-from-external-load-balancers=
<b>node2</b>   Ready    <none>          32m   v1.27.2   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,<b>capacity=low</b>,kubernetes.io/arch=amd64,kubernetes.io/hostname=node2,kubernetes.io/os=linux
node3   Ready    <none>          29m   v1.27.2   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,capacity=high,kubernetes.io/arch=amd64,kubernetes.io/hostname=node3,kubernetes.io/os=linux
</pre>

```
[node1 ~]$ kubectl get all
NAME        READY   STATUS    RESTARTS   AGE
pod/nginx   1/1     Running   0          16m

NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   35m
```

+ ### NodeAffinity
Containts will go here....


## 6. Pod
Containts will go here....


## 7. Service
Containts will go here....

## 8. Deployment
Containts will go here....


## 9. Ingress
Containts will go here....

> Dorothy followed her through many of the beautiful rooms in her castle.
>
>> The Witch bade her clean the pots and kettles and sweep the floor and keep the fire fed with wood.

kkkk

> #### The quarterly results look great!
>
> - Revenue was off the chart.
> - Profits were higher than ever.
>
>  *Everything* is going according to **plan**.
