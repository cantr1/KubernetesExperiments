# Kubernetes Notes
## General Notes
### Pods
A pod is the smallest deployable unit of compute that you can create and manage with K8s.

Every Pod in a Kubernetes cluster has a unique internal-to-k8s IP address. By giving each Pod a unique IP, Kubernetes simplifies communication and service discovery within the cluster. Pods within the same Node or across different Nodes can easily communicate.

All the resources inside a k8s cluster are virtualized. So, the IP address of a Pod is not the same as the IP address of the Node it's running on. It's a virtual IP address that is only accessible from within the cluster.

### Deployments
A Deployment provides declarative updates for Pods and ReplicaSets.

You describe your desired state in a Deployment, and the Deployment Controller's job is to make the current state match the desired state. You declare your hopes and dreams, and it's Kubernetes' job to make them come true.

### Thrashing Pods
One of the most common problems you'll run into when working with Kubernetes is Pods that keep crashing and restarting. This is called "thrashing" and it's usually caused by one of a few things:

The application recently had a bug introduced in the latest image version
The application is misconfigured and can't start properly
A dependency of the application is misconfigured and the application can't start properly
The application is trying to use too much memory and is being killed by Kubernetes

### Services
Services provide a stable endpoint for pods. They are an abstraction used to provide a stable endpoint and load balance traffic across a group of Pods.

### Persistent Volumes
Instead of simply adding a volume to a deployment, a persistent volume is a cluster-level resource that is created separately from the pod and then attached to the pod. It's similar to a ConfigMap in that way.

PVs can be created statically or dynamically.

Static PVs are created manually by a cluster admin
Dynamic PVs are created automatically when a pod requests a volume that doesn't exist yet
Generally speaking, and especially in the cloud-native world, we want to use dynamic PVs. It's less work and more flexible.

### Namespaces
Namespaces are a way to isolate cluster resources into groups. They're a bit like directories on your computer, but instead of containing files, they contain Kubernetes objects. 

You can only use a name once. It is a unique identifier. That's how kubectl apply knows when it should create a new resource and when it should update an existing one. Namespaces allow us to use the same name for different resources, as long as they're in different namespaces.

### Metrics
Install the following:
`minikube addons enable metrics-server`

Then run `kubectl top pod`

---
## Commands
To create a deployment, this creates a pod with the name built from the docker image
`kubectl create deployment synergychat-web --image=docker.io/bootdotdev/synergychat-web:latest`

To view deployments
`kubectl get deployments`

To port forward the deployment:
`kubectl port-forward PODNAME 8080:8080`

To get a list of running pods:
`kubectl get pods`

Print the logs (what the container is printing to stdout):
`kubectl logs PODNAME`

Kill a pod (this might take several seconds to complete):
`kubectl delete pod PODNAME`

To get more info on pods:
`kubectl get pods -o wide`

To view the deployment file:
`kubectl get deployment NAME -o yaml`

To edit deployment file:
`kubectl edit deployment NAME`

To get replicatsets:
`kubectl get replicasets`

To apply a static config to the deployment:
`kubectl apply -f web-deployment.yaml`

To get active services:
`kubectl get services`
You would then port forward the service:
`kubectl port-forward service/web-service 8080:80`

Open local cluster to localmachine:
`minikube tunnel -c`

Get PVC info
```
kubectl get pvc
kubectl get pv
```

Create namespace
`kubectl create ns crawler`

Get namespaces
`kubectl get ns`

Working with name spaces:
```
kubectl -n crawler get pods
kubectl -n crawler get svc
kubectl -n crawler get configmaps
```