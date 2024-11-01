# Learn Kubernetes

We're using [minikube](https://minikube.sigs.k8s.io/docs/) to learn [kubernetes](https://kubernetes.io/).

```
Kubernetes, also known as K8s, is an open-source system for automating deployment, scaling, and management of containerized applications.
```

## Concepts

A pod (application) is the smallest computing unit deployable in kubernetes, it's just a wrapper of a docker container.

A node (machine) is a fisical or virtual computer that runs pods.

A cluster is a group of nodes.

Kubernetes figures out where to place pods based on how what resources they need.

You declare a "desired" state and kubernetes makes sure that this state is always true, if I set 2 replicas kubernetes will always try to have 2 pods running for my deployment, even if I trash one.

Kubernetes is all about building self-healing systems and will always try to restart containers.

We manage env vars with ConfigMaps, reference a configmap inside a deployment to set an env inside a container. Configmaps are not secure since they aren't encrypted, don't store credentials in there, to store secrets use Kubernetes Secrets or other third party services.

## Kubectl commands

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
- kubectl apply -f deployment.yaml
- kubectl get configmaps

## Minikube commands

- minikube version
- minikube start --extra-config "apiserver.cors-allowed-origins=["http://example.com"]"
- minikube dashboard --port=PORT
