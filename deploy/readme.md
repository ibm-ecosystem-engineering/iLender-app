# iLender Application Deployment

Here is the instruction to deploy the application in the Kubernetes cluster.

### Apply Yaml

Apply application resource yamls in the Kubernetes cluster to deploy the application.

```
kubectl apply -f ./yaml
```

Application get installed in `ilender-ns` namespace.


### Get External IP of the cluster

Run the below command to retrieve `EXTERNAL-IP` from node .

```
kubectl get nodes -o wide
```

Here would be the output. The `EXTERNAL-IP` column shows the external-ips `1.1.1.1`   and `1.2.3.5`.

```
Jeyas-MacBook-Pro:frontuiservice jeyagandhi$ kubectl get nodes -o wide
NAME             STATUS   ROLES    AGE   VERSION       INTERNAL-IP      EXTERNAL-IP       OS-IMAGE             KERNEL-VERSION       CONTAINER-RUNTIME
10.241.253.157   Ready    <none>   26d   v1.20.7+IKS   10.241.253.157   1.1.1.1   Ubuntu 18.04.5 LTS   4.15.0-144-generic   containerd://1.4.6
10.241.253.189   Ready    <none>   26d   v1.20.7+IKS   10.241.253.189   1.2.3.5   Ubuntu 18.04.5 LTS   4.15.0-144-generic   containerd://1.4.6
```

### Get NodePort of the service.

Run the below command to get the `NodePort` of the `ilender-frontweb` service

```
kubectl get svc
```

Here would be the output. The value is `30500`.

```
Jeyas-MacBook-Pro:frontuiservice jeyagandhi$ kubectl get svc
NAME                      TYPE           CLUSTER-IP       EXTERNAL-IP     PORT(S)          AGE
ilender-bigbank           LoadBalancer   172.21.165.179   1.1.1.1         9090:30598/TCP   10d
ilender-creditscore       NodePort       172.21.55.156    <none>          9090:30501/TCP   10d
ilender-customerprofile   LoadBalancer   172.21.145.229   1.1.1.1         9090:32751/TCP   10d
ilender-frontweb          NodePort       172.21.44.159    <none>          9090:30500/TCP   10d
ilender-greatbank         LoadBalancer   172.21.84.144    <pending>       9090:31622/TCP   10d
ilender-loan              LoadBalancer   172.21.161.226   1.1.1.1         9090:30301/TCP   10d
ilender-loanprocessor     LoadBalancer   172.21.82.15     1.1.1.1         9090:30880/TCP   10d
ilender-openbanking       LoadBalancer   172.21.235.41    1.1.1.1         9090:31331/TCP   10d
ilender-user              LoadBalancer   172.21.43.214    1.1.1.1         9090:32427/TCP   10d
```

### 3. Access the Application

You can access the application using the `EXTERNAL-IP` from node and `NodePort` from svc like this

```
  http://<<EXTERNAL-IP>>:<<NodePort>>
```

ex:

```
  http://1.1.1.1:30500
```

#### Users
Here are the users to access.

```
sam/sam     (business manager)
sandy/sandy (smb customer)
