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