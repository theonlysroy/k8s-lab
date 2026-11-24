# k8s-lab

Disposable single-node Kubernetes (kind) + Portainer, driven by `make`.

Requires: docker, kind, kubectl (kustomize is built into kubectl).

    make up      # cluster + portainer + sample app
    make test    # nginx at http://localhost:8080
    make down    # destroy everything
    make help    # all targets

Portainer: https://localhost:9443 (set the admin password within ~5 min of
first start, otherwise `make ui-down ui`). Kind nodes show up as containers.

Layout:
    cluster/   kind config (K8s version pinned)
    compose/   portainer
    k8s/       manifests, applied with kustomize
