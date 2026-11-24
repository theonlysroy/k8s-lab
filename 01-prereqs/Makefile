CLUSTER ?= dev
CLUSTER_MULTI ?=dev-multinode
KUBECTL := kubectl --context kind-$(CLUSTER)
COMPOSE := docker compose -f compose/docker-compose.yaml

.DEFAULT_GOAL := help
.PHONY: help up down reset cluster cluster-multinode cluster-down ui ui-down deploy undeploy status logs test

help:  ## show targets
	@grep -E '^[a-z-]+:.*##' $(MAKEFILE_LIST) | awk -F':.*## ' '{printf "  %-14s %s\n", $$1, $$2}'

# up: cluster ui deploy  ## cluster + portainer + app
up: cluster ui
down: ui-down cluster-down  ## destroy everything
reset: down up  ## clean slate

cluster:  ## create kind cluster
	kind create cluster --config cluster/kind.yaml

cluster-multinode:
	kind create cluster --config cluster/kind-multinode.yaml

cluster-multinode-down:
	kind delete cluster --nmae $(CLUSTER_MULTI)

cluster-down:  ## delete kind cluster
	kind delete cluster --name $(CLUSTER)

ui:  ## start portainer at https://localhost:9443
	$(COMPOSE) up -d

ui-down:  ## stop portainer and delete its data
	$(COMPOSE) down -v

deploy:  ## apply k8s/ manifests
	$(KUBECTL) apply -k k8s/
	$(KUBECTL) -n lab rollout status deploy/web

undeploy:  ## remove the app only
	$(KUBECTL) delete -k k8s/ --ignore-not-found

status:  ## nodes and app resources
	$(KUBECTL) get nodes
	$(KUBECTL) -n lab get all

logs:  ## tail app logs
	$(KUBECTL) -n lab logs -l app=web --tail=50 -f

test:  ## curl the app at localhost:8080
	curl -sI http://localhost:8080 | head -1
