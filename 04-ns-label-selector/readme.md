## namespace

In kubernetes there is no formal grouping of resources by design. Each resource in a cluster is independent and isolated.

Namespace provide logical partioning and grouping of resources inside the cluster. It's like a logical cluster within our cluster.

It allows
- name scoping
- policy boundary
- RBAC, resource quota and network policies

_it does not actually make any groups or paritions. Its logical_

**Things to know:**

Not everything is namespaced. Nodes, PVs, StorageClasses, ClusterRoles, and Namespaces themselves are cluster-scoped. Check with `kubectl api-resources --namespaced=false`.
Cross-namespace DNS: api.dev.svc.cluster.local. Within the same namespace, plain api works.
A namespace is not a security boundary by itself. Without NetworkPolicies, pods in any namespace can talk to each other.


## labels

key/value tags attached to objects like Pods as metadata. Intended to specify identifying attributes to the object that are meaningful and relevant to the users.

eg. `"environment": "dev"`, `"release": "stable"`

- prefix (optional) must be a DNS subdomain
- `app.kubernetes.io/instance` -- example prefix and name of the label


## selectors

Lable selectors are for querying group of objects using the labels. Since labels are not unique and multiple objects can be using same labels; selectors thus query for a set of objects

- equality based selection

```bash
kubectl get pods -l env=dev
kubectl get pods -l app=api,env=dev
kubectl get pods -l app!=client
kubectl get pods --show-labels

```

- set based selection

```bash
kubectl get pods -l 'env in (dev,staging)'
kubectl get pods -l 'tier notin (frontend)'
kubectl get pods -l 'app'                # label exists
kubectl get pods -l '!canary'            # label doesn't exist
```
