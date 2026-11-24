
```bash
kubectl get nodes
kubectl get nodes -o wide

kubectl config get-contexts
kubectl config use-context [cluster_name]

# Create nginx pod
kubectl run nginx-pod --image=nginx:latest

kubectl explain pod
kubectl apply -f [config_file]

kubectl describe pod [pod_name]
kubectl edit pod [pod_name]

kubectl exec -it [pod_name] -- sh

kubectl run nginx --image=nginx --dry-run=client
kubectl run nginx --image=nginx --dry-run=client -o yaml > pod.yaml

````

### Basics of yaml

```yaml

apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    env: demo
    type: frontend
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80

```
