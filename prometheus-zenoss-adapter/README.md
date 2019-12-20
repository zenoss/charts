# prometheus-zenoss-adapter

[prometheus-zenoss-adapter] is an agent that collects metrics from a Kubernetes
cluster and sends them to [Zenoss].

## Basic Usage

```bash
$ helm repo add zenoss https://zenoss.github.io/charts/
$ helm install zenoss/prometheus-zenoss-adapter \
    --set zenoss.source=<K8S_CLUSTER_NAME> \
    --set zenoss.apiKey=<ZENOSS_API_KEY>
```

## Introduction

This chart installs prometheus-zenoss-adapter on a [Kubernetes] cluster using
the [Helm] package manager.

## Prerequisites

- Kubernetes 1.8+
- Helm

See the [Helm Quickstart Guide] if you don't already have Helm running on your
cluster.

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm repo add zenoss https://zenoss.github.io/charts/
$ helm install zenoss/prometheus-zenoss-adapter \
    --name my-release \
    --set zenoss.source=<K8S_CLUSTER_NAME> \
    --set zenoss.apiKey=<ZENOSS_API_KEY>
```

This command deploys prometheus-zenoss-adapter on the Kubernetes cluster in the
default configuration. The [configuration](#configuration) section lists the
parameters that can be configured during installation.

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
$ helm delete my-release
```

This command removes all of the Kubernetes components associated with the chart
and deletes the release.

## Configuration

| Parameter                                  | Description                                                                  | Default                            |
| ------------------------------------------ | ---------------------------------------------------------------------------- | ---------------------------------- |
| `zenoss.source`                            | Set a unique name for the prometheus data source in Zenoss                   | `nil`                              |
| `zenoss.name`                              | Arbitrary name for Zenoss endpoint to differentiate it from others           | `default`                          |
| `zenoss.address`                           | Zenoss API endpoint address: <name>:<port>                                   | `api.zenoss.io:443`                |
| `zenoss.apiKey`                            | Zenoss API key                                                               | `nil`                              |
| `zenoss.apiKeyExistingSecret`              | Existing Kubernetes secret containing Zenoss API key in `api-key` key        | `nil`                              |
| `zenoss.devMode`                           | Enable development mode                                                      | `false`                            |
| `image.repository`                         | Image repository                                                             | `zenoss/prometheus-zenoss-adapter` |
| `image.tag`                                | Image tag                                                                    | `latest`                           |
| `image.pullPolicy`                         | Image pull policy                                                            | `IfNotPresent`                     |
| `image.pullSecrets`                        | Docker registry secret names as an array                                     | `[]`                               |
| `resources`                                | CPU/Memory resource requests/limits                                          | `{}`                               |
| `nodeSelector`                             | Node labels for pod assignment                                               | `{}`                               |
| `tolerations`                              | Toleration labels for pod assignment                                         | `[]`                               |
| `affinity`                                 | Map of node/pod affinities                                                   | `{}`                               |
| `nameOverride`                             | String to partially override fullname template                               | `nil`                              |
| `fullnameOverride`                         | String to fully override fullname template                                   | `nil`                              |

Specify each parameter using the `--set key=value[,key=value]` argument to
`helm install`. For example:

```console
$ helm install \
    --name my-release \
    --set zenoss.source=<K8S_CLUSTER_NAME> \
    --set zenoss.apiKey=<ZENOSS_API_KEY> \
    zenoss/prometheus-zenoss-adapter
```

The above command sets the minimum required parameters to install.

Alternatively, a YAML file that specifies the values for the parameters can be
provided while installing the chart. For example:

```console
$ helm install --name my-release -f values.yaml zenoss/prometheus-zenoss-adapter
```

[Helm]: https://helm.sh/
[Helm Quickstart Guide]: https://helm.sh/docs/using_helm/#quickstart
[Kubernetes]: https://kubernetes.io/
[Zenoss]: https://www.zenoss.com/
[prometheus-zenoss-adapter]: https://github.com/zenoss/prometheus-zenoss-adapter
