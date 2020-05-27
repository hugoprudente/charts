# Foundry VTT

[![FoundryVTT Version: v0.6.0](https://img.shields.io/badge/foundry-v0.6.0-brightgreen?logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA4AAAAOCAYAAAAfSC3RAAAAAXNSR0IArs4c6QAAAIRlWElmTU0AKgAAAAgABQESAAMAAAABAAEAAAEaAAUAAAABAAAASgEbAAUAAAABAAAAUgEoAAMAAAABAAIAAIdpAAQAAAABAAAAWgAAAAAAAABIAAAAAQAAAEgAAAABAAOgAQADAAAAAQABAACgAgAEAAAAAQAAAA6gAwAEAAAAAQAAAA4AAAAATspU+QAAAAlwSFlzAAALEwAACxMBAJqcGAAAAVlpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IlhNUCBDb3JlIDUuNC4wIj4KICAgPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4KICAgICAgPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIKICAgICAgICAgICAgeG1sbnM6dGlmZj0iaHR0cDovL25zLmFkb2JlLmNvbS90aWZmLzEuMC8iPgogICAgICAgICA8dGlmZjpPcmllbnRhdGlvbj4xPC90aWZmOk9yaWVudGF0aW9uPgogICAgICA8L3JkZjpEZXNjcmlwdGlvbj4KICAgPC9yZGY6UkRGPgo8L3g6eG1wbWV0YT4KTMInWQAAAiFJREFUKBVVks1rE1EUxc+d5tO0prZVSZsUhSBIPyC02ooWurJ0I7rQlRvdC/4N4h9gt7pyoRTswpWgILgQBIOIiC340VhbpC0Ek85MGmPmXc+baWpNGJg77/7uOffeB+z9FHB0FrH9eLwwqpOF0f34KrpsTicW+6L8KE8QhO/n8n1IOgtQHYZA+a/Ai9+Wd6v1g7liq5A2OjKSQNa9hkO4hAzOIylf6CHALk6hoWXsylPkfjyyApaJhVCxmERy5zLSuI7D8h1H5BWht1aBhS6wdI3pN7GabyuyS4JPrchzujmNjDxAVrrRL2PoxRSGxOfjssgEjkkJvVJBWu6h5M7YenvDoOO0OgicD4TPIKWbBG6xvwTaKCMwSU7hKxK6gt8mbsFIMaF5iDyjUg6iPnqc58higCr9fD4iTvWMziAmK2g73f/AADVWX0YXrlChirgOcqL3WXYBYpTfUuxzjkW30dI1C0ZW1RnjMopo4C56MIs6CgQrMER2cJoz9zjdO2iz17g2yZUjqzHWbuA4/ugiEz7DVRe/aLxmcvDQ5Cq+oWGWeDbAgiETXgArrVOFGzR0EkclxrVMcpfLgFThY5roe2yz95ZZkzcbj22+w2VG8Pz6Q/b5Gr6uM9mw04uo6ll4tOlhE8a8xNzGYihCJoT+u3I4kUIp6OM0X9CHHds8frbqsrXlh9CB62nj8L5a9Y4DHR/K68TgcHhoz607Qp34L72X0rdSdM+vAAAAAElFTkSuQmCC)](https://foundryvtt.com/releases/0.6.0)
[![Known Vulnerabilities](https://snyk.io/test/github/hugoprudente/charts/badge.svg)](https://snyk.io/test/github/hugoprudente/charts)

[Foundry VTT](http://foundryvtt.com/) is a standalone application built for experiencing multiplayer tabletop RPGs using a feature-rich and modern self-hosted application where your players connect directly through the browser.
## Introduction

You can get a [FoundryVTT](https://foundryvtt.com) instance up and running in
minutes using this chart and Felddy [foundryvtt-docker](https://github.com/felddy/foundryvtt-docker) Docker container.

## Prerequisites

- 512 MB of RAM
- Kubernetes 1.4+ with Beta APIs enabled
- PV provisioner support in the underlying infrastructure

## Installing the Chart

To install the chart with the release name `my-release`, run:

```bash
$ helm install --name my-release ./incubator/foundry-vtt
```

This command deploys a Foundry VTT dedicated server with sensible defaults.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
$ helm uninstall my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

Refer to [values.yaml](values.yaml) for the full run-down on defaults. These are a mixture of Kubernetes and Foundry VTT-related directives that map to environment variables in the [Foundry VTT](https://github.com/felddy/foundryvtt-docker) Docker image by Felddy.

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```bash
$ helm install --name my-release \
    --set foundryvtt.adminKey='MyPa$$word' \
    ./incubator/foundry-vtt
```

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install --name my-release -f values.yaml ./incubator/foundry-vtt
```

> **Tip**: You can use the default [values.yaml](values.yaml)

## Persistence

The [Foundry VTT Docker](https://github.com/hugoprudente/foundryvtt-docker) image needs to be built and published to private registry, stores the saved games and mods under /data.

By default a PersistentVolumeClaim is created and mounted for saves but not mods. In order to disable this functionality

you can change the values.yaml to disable persistence under the sub-sections under `persistence`.

> *"An emptyDir volume is first created when a Pod is assigned to a Node, and exists as long as that Pod is running on that node. When a Pod is removed from a node for any reason, the data in the emptyDir is deleted forever."*

## TLS with Cert Manager

### Install the CustomResourceDefinition resources separately
```
kubectl apply -f https://raw.githubusercontent.com/jetstack/cert-manager/release-0.12/deploy/manifests/00-crds.yaml
```

> **Important:**
> If you are running Kubernetes v1.15 or below, you will need to add the `--validate=false flag to your kubectl apply command above else you will receive a validation error relating to the x-kubernetes-preserve-unknown-fields field in cert-manager’s CustomResourceDefinition resources. This is a benign error and occurs due to the way kubectl performs resource validation.

### Create the namespace for cert-manager
```
kubectl create namespace cert-manager
```

### Add the Jetstack Helm repository
```
helm repo add jetstack https://charts.jetstack.io
```

### Update your local Helm chart repository cache
```
helm repo update
```

### Install the cert-manager Helm chart
```
helm install \
  cert-manager jetstack/cert-manager \
  --namespace cert-manager \
  --version v0.12.0
```

kubectl get pods --namespace cert-manager
```
NAME                                       READY   STATUS    RESTARTS   AGE
cert-manager-5c6866597-zw7kh               1/1     Running   0          2m
cert-manager-cainjector-577f6d9fd7-tr77l   1/1     Running   0          2m
cert-manager-webhook-787858fcdb-nlzsq      1/1     Running   0          2m
```