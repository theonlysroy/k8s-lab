## Commands

```bash
# check docker version v29.10.0
docker --version
docker version --format '{{.Server.Version}}'

# docker resources check
docker image ls --no-trunc
docker ps -a --no-trunc

# check kubectl version, v1.37.2
kubectl version 

# list all the kind clusters
kind get clusters
kubectl get nodes # get the nodes -- kind has only one node
kubectl get nodes -o wide

# create kind cluster
kind create cluster --name=03lab --image=kindest/node

# create kind cluster from config file
kind create cluster --config kind-example-config.yaml

# get any resource
kubectl get [resource]
kubectl get pods
kubectl get nodes
kubectl get deployment

# get any resource from namespace
kubectl get nodes,pods,deployment,service -n [namespace]
kubectl get nodes,pods,deployment,service --all-namespaces

# describe
kubectl describe pod pod-name -n=default
kubectl describe pod pod-name -n default
kubectl describe pod/pod-name -n=default
kubectl describe pod/pod-name -n default

# get any resource data in wide format
kubectl get pod -o wide
kubectl get pods -o wide
kubectl get pod -o -n kube-system | awk '{print $1, "\t", $6}'

```
