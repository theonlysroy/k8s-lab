## replicaset

it's a kubernetes resource/object whose purpose is to maintain a stable set of replica Pods running at a given time.

- changing the image in the template doesn't touch existing pods
- only fixes the count, not the version
- New pods get the new image and old ones stay as they are
- Selector-based adoption: the RS owns any pod whose labels match, even one you created by hand
- Selector must match `template.metadata.labels`, or the apply is rejected. The selector is immutable after creation.

## deployment

it manages a set of Pods to run an application workload

- it creates and owns the ReplicaSets
- same YAML shape as RS, `kind: Deployment`
- pod-template-hash labels is how RS matches pod apart from other version
- rollout only triggers when `.spec.template` changes
- changing `replicas` scales up/down the current RS; no new version
- annotate rollout `kubectl annotate`
- `deployment controller` is the service that checks the deployment current state via api server and maintains the desired state declared

> it's for stateless apps. Stateful ones (database) use StatefulSets
