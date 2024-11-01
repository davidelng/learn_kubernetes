# Learn Kubernetes

We're using [minikube](https://minikube.sigs.k8s.io/docs/) to learn [kubernetes](https://kubernetes.io/).

```
Kubernetes, also known as K8s, is an open-source system for automating deployment, scaling, and management of containerized applications.
```

## Concepts

A pod (application) is the smallest computing unit deployable in kubernetes, it's just a wrapper of a docker container.

A node (machine) is a fisical or virtual computer that runs pods.

A cluster is a group of nodes.

Everything (like pods or services) in a kubernetes cluster has an internal IP.

### Deployments

Kubernetes figures out where to place pods based on how what resources they need.

You declare a "desired" state and kubernetes makes sure that this state is always true, if I set 2 replicas kubernetes will always try to have 2 pods running for my deployment, even if I trash one.

Kubernetes is all about building self-healing systems and will always try to restart containers.

### Configmaps

We manage env vars with ConfigMaps, reference a configmap inside a deployment to set an env inside a container.

Configmaps are not secure since they aren't encrypted, don't store credentials in there, to store secrets use Kubernetes Secrets or other third party services.

### Services

Services provide a stable endpoint and load balancing across pods. The service will always be available at a given URL, even if the pod is destroyed and recreated.

A service will continuously scan for pods matching its selector name and add them to its pool.

There are several type of services:

- ClusterIP = exposes the service to applications within the cluster
- NodePort = exposes the Service on each Node's IP at a static port
- LoadBalancer = creates an external load balancer in the current cloud environment and assigns a fixed external IP to the service
- ExternalName = map your cluster's DNS server to return a CNAME record with externalName host value

services are built on top of each other (a LoadBalancer is built on a NodePort that is built on a ClusterIP).

ClusterIP are meant to be accessed within the cluster, while NodePort and LoadBalancer are used when you expose a service to the outside world. ExternalName is used for DNS.

### Ingresses

To expose applications to the outside world sometimes an Ingress object is used instead of a NodePort because it also allows you to host multiple services on the same IP or same port, terminate SSL and integrate with external DNS.

Ingresses are used in production environments.

## Commands used

## Kubectl

- kubectl version
- kubectl create deployment NAME --image=DOCKERIMAGE
- kubectl get deployments -o yaml
- kubectl edit deployment NAME
- kubectl get pods -o wide
- kubectl port-forward PODNAME 8080:8080
- kubectl proxy
- kubectl logs PODNAME
- kubectl delete pod PODNAME
- kubectl get replicasets
- kubectl apply -f FILE
- kubectl get configmaps
- kubectl get (svc|service) NAME -o yaml

## Minikube

- minikube version
- minikube start --extra-config "apiserver.cors-allowed-origins=["http://example.com"]"
- minikube dashboard --port=PORT
- minikube addons enable ingress
- minikube tunnel -c
