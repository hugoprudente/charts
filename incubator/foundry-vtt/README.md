# Foundry VTT

<!-- BADGES/ -->
[![FoundryVTT Version: v0.6.6](https://img.shields.io/badge/foundry-v0.6.6-brightgreen?logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA4AAAAOCAYAAAAfSC3RAAAAAXNSR0IArs4c6QAAAIRlWElmTU0AKgAAAAgABQESAAMAAAABAAEAAAEaAAUAAAABAAAASgEbAAUAAAABAAAAUgEoAAMAAAABAAIAAIdpAAQAAAABAAAAWgAAAAAAAABIAAAAAQAAAEgAAAABAAOgAQADAAAAAQABAACgAgAEAAAAAQAAAA6gAwAEAAAAAQAAAA4AAAAATspU+QAAAAlwSFlzAAALEwAACxMBAJqcGAAAAVlpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IlhNUCBDb3JlIDUuNC4wIj4KICAgPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4KICAgICAgPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIKICAgICAgICAgICAgeG1sbnM6dGlmZj0iaHR0cDovL25zLmFkb2JlLmNvbS90aWZmLzEuMC8iPgogICAgICAgICA8dGlmZjpPcmllbnRhdGlvbj4xPC90aWZmOk9yaWVudGF0aW9uPgogICAgICA8L3JkZjpEZXNjcmlwdGlvbj4KICAgPC9yZGY6UkRGPgo8L3g6eG1wbWV0YT4KTMInWQAAAiFJREFUKBVVks1rE1EUxc+d5tO0prZVSZsUhSBIPyC02ooWurJ0I7rQlRvdC/4N4h9gt7pyoRTswpWgILgQBIOIiC340VhbpC0Ek85MGmPmXc+baWpNGJg77/7uOffeB+z9FHB0FrH9eLwwqpOF0f34KrpsTicW+6L8KE8QhO/n8n1IOgtQHYZA+a/Ai9+Wd6v1g7liq5A2OjKSQNa9hkO4hAzOIylf6CHALk6hoWXsylPkfjyyApaJhVCxmERy5zLSuI7D8h1H5BWht1aBhS6wdI3pN7GabyuyS4JPrchzujmNjDxAVrrRL2PoxRSGxOfjssgEjkkJvVJBWu6h5M7YenvDoOO0OgicD4TPIKWbBG6xvwTaKCMwSU7hKxK6gt8mbsFIMaF5iDyjUg6iPnqc58higCr9fD4iTvWMziAmK2g73f/AADVWX0YXrlChirgOcqL3WXYBYpTfUuxzjkW30dI1C0ZW1RnjMopo4C56MIs6CgQrMER2cJoz9zjdO2iz17g2yZUjqzHWbuA4/ugiEz7DVRe/aLxmcvDQ5Cq+oWGWeDbAgiETXgArrVOFGzR0EkclxrVMcpfLgFThY5roe2yz95ZZkzcbj22+w2VG8Pz6Q/b5Gr6uM9mw04uo6ll4tOlhE8a8xNzGYihCJoT+u3I4kUIp6OM0X9CHHds8frbqsrXlh9CB62nj8L5a9Y4DHR/K68TgcHhoz607Qp34L72X0rdSdM+vAAAAAElFTkSuQmCC)](https://foundryvtt.com/releases/0.6.6)
[![GitHub Charts](https://github.com/hugoprudente/charts/workflows/Lint%20and%20Test%20Charts/badge.svg)](https://github.com/hugoprudente/charts/actions/)
[![Patreon](https://img.shields.io/badge/patreon-donate-yellow.svg)](https://patreon.com/nerdweekoficial)
[![GitHub license](https://img.shields.io/github/license/hugoprudente/charts)](https://github.com/hugoprudente/charts/blob/master/LICENSE)
[![GitHub forks](https://img.shields.io/github/forks/hugoprudente/charts)](https://github.com/hugoprudente/charts/network)
[![GitHub stars](https://img.shields.io/github/stars/hugoprudente/charts)](https://github.com/hugoprudente/charts/stargazers)

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

### Values Configurations  ###

| Parameter  | Description | Default |
|-------|---------|---------|
| foundryvtt.adminKey | Admin password to be applied at startup.  If omitted the admin password will be cleared. | admin |
| foundryvtt.awsConfig | An absolute or relative path that points to the [awsConfig.json](https://foundryvtt.com/article/aws-s3/) or `true` for AWS environment variable [credentials evaluation](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/setting-credentials-node.html) usage | null |
| foundryvtt.hostname | A custom hostname to use in place of the host machine's public IP address when displaying the address of the game session. This allows for reverse proxies or DNS servers to modify the public address. | foundry.domain.com |
| foundryvtt.noUpdate | Prevent the application from being updated from the web interface.  The application code is immutable when running in a container.  See the [Updating](#updating) section for the steps needed to update this container. | true |
| foundryvtt.proxyPort | Inform the Foundry Server that the software is running behind a reverse proxy on some other port. This allows the invitation links created to the game to include the correct external port. | 80 |
| foundryvtt.proxySSL | Indicates whether the software is running behind a reverse proxy that uses SSL. This allows invitation links and A/V functionality to work as if the Foundry Server had SSL configured directly. | true |
| foundryvtt.routePrefix | A string path which is appended to the base hostname to serve Foundry VTT content from a specific namespace. For example setting this to `demo` will result in data being served from `http://x.x.x.x:30000/demo/`. | null |
| foundryvtt.sslCert | An absolute or relative path that points towards a SSL certificate file which is used jointly with the sslKey option to enable SSL and https connections. If both options are provided, the server will start using HTTPS automatically. | null |
| foundryvtt.sslKey | An absolute or relative path that points towards a SSL key file which is used jointly with the sslCert option to enable SSL and https connections. If both options are provided, the server will start using HTTPS automatically. | null |
| foundryvtt.updateChannel | The update channel to subscribe to.  "alpha", "beta", or "release". | "release" |
| foundryvtt.upnp | Allow Universal Plug and Play to automatically request port forwarding for the Foundry VTT port to your local network address. | false |
| foundryvtt.world | The world startup at system start. | null |

## Persistence

The [Foundry VTT Docker](https://github.com/hugoprudente/foundryvtt-docker) image needs to be built and published to private registry, stores the saved games and mods under /data.

By default a PersistentVolumeClaim is created and mounted for saves but not mods. In order to disable this functionality

you can change the values.yaml to disable persistence under the sub-sections under `persistence`.

> *"An emptyDir volume is first created when a Pod is assigned to a Node, and exists as long as that Pod is running on that node. When a Pod is removed from a node for any reason, the data in the emptyDir is deleted forever."*

## TLS ingress-nginx and Cert Manager

### Setting up `ingress-nginx` as is required.

```
kubectl create ns ingress-nginx
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/nginx-0.30.0/deploy/static/mandatory.yaml
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/nginx-0.30.0/deploy/static/provider/cloud-generic.yaml
```

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
> **Important:**
> If you are running Kubernetes v1.15 or below, you will need to add the `--validate=false flag to your kubectl apply command above else you will receive a validation error relating to the x-kubernetes-preserve-unknown-fields field in cert-manager’s CustomResourceDefinition resources. This is a benign error and occurs due to the way kubectl performs resource validation. Reference official [documentation](https://cert-manager.io/docs/installation/kubernetes/)

```
helm install \
  cert-manager jetstack/cert-manager \
  --namespace cert-manager\ 
  --version v0.15.1 
```

```
kubectl get pods --namespace cert-manager
NAME                                       READY   STATUS    RESTARTS   AGE
cert-manager-5c6866597-zw7kh               1/1     Running   0          2m
cert-manager-cainjector-577f6d9fd7-tr77l   1/1     Running   0          2m
cert-manager-webhook-787858fcdb-nlzsq      1/1     Running   0          2m
```

### Checking emited certificate 

```
kubectl get certificates
NAME                      READY   SECRET                    AGE
tls-foundry-vtt-ingress   True    tls-foundry-vtt-ingress   34m
```

```
kubectl describe certificate tls-foundry-vtt-ingress
Events:
  Type    Reason        Age   From          Message
  ----    ------        ----  ----          -------
  Normal  GeneratedKey  35m   cert-manager  Generated a new private key
  Normal  Requested     35m   cert-manager  Created new CertificateRequest resource "tls-foundry-vtt-ingress-1297638063"
  Normal  Issued        22m   cert-manager  Certificate issued successfully
```

## Backup & Backup Restauration

Identifying the pod

```bash
kubectl get pods --namespace foundry-vtt
NAME                                   READY   STATUS    RESTARTS   AGE
foundry-vtt-5b5864c7bc-v6r7d           1/1     Running   0          5d5h
```

Generating the backup on the /tmp/ directory.

```bash
kubectl exec -it foundry-vtt-5b5864c7bc-v6r7d -- /bin/sh -c "cd /data && tar -cvzf /data/backup.tar.gz Data"
```

Output:

```log
Data/
Data/worlds/
Data/worlds/README.txt
Data/worlds/waterdeep/
Data/worlds/waterdeep/world.json
Data/worlds/waterdeep/scenes/
Data/worlds/waterdeep/
Data/worlds/the-masters-vault/
...
Data/assets/characters/tiefling_bard.png
Data/assets/handout/
Data/assets/handout/ellaria_will.png
Data/assets/handout/ellarias_memory.jpg
Data/assets/tiles/
Data/assets/tiles/alcaeus_home.png
Data/assets/tiles/helenes_grave.png
Data/assets/tiles/vixthras_lair.png
```

Downloading the backup!

```bash
kubectl cp foundry-vtt-5b5864c7bc-v6r7d:/data/backup.tar.gz backup.tar.gz
backup.tar.gz
```

Resauring a Backup!
```bash
kubectl cp backup.tar.gz nerdweek-foundry-vtt-ddc84f8b5-dkz4c:/data/backup.tar.gz
kubectl exec -it  nerdweek-foundry-vtt-ddc84f8b5-dkz4c -- /bin/sh -c "cd /data/ && tar -xvzf backup.tar.gz && rm -v /data/backup.tar.gz"
```

Output:

```log
Data/
Data/worlds/
Data/worlds/README.txt
Data/worlds/waterdeep/
...
Data/assets/handout/ellarias_memory.jpg
Data/assets/tiles/
Data/assets/tiles/alcaeus_home.png
Data/assets/tiles/helenes_grave.png
Data/assets/tiles/vixthras_lair.png
removed '/data/backup.tar.gz'
```
