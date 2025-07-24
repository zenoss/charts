# zenoss-agent-kubernetes

[zenoss-agent-kubernetes] is an agent that collects metrics from a Kubernetes
cluster and sends them to [Zenoss].

## Basic Usage

```bash
$ helm repo add zenoss https://zenoss.github.io/charts/
$ helm install MY_RELEASE_NAME zenoss/zenoss-agent-kubernetes \
    --set zenoss.clusterName=<K8S_CLUSTER_NAME> \
    --set zenoss.apiKey=<ZENOSS_API_KEY>
    --set zenoss.address=<ZENOSS_API_ADDRESS>
```

## Introduction

This chart installs zenoss-agent-kubernetes on a [Kubernetes] cluster using
the [Helm] package manager.

## Prerequisites

- Kubernetes 1.8+
- [Kubernetes Metrics Server]
- Helm

See the [Helm Quickstart Guide] if you don't already have Helm running on your
cluster.

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm repo add zenoss https://zenoss.github.io/charts/
$ helm install zenoss/zenoss-agent-kubernetes \
    --name my-release \
    --set zenoss.clusterName=<K8S_CLUSTER_NAME> \
    --set zenoss.apiKey=<ZENOSS_API_KEY>
```

This command deploys zenoss-agent-kubernetes on the Kubernetes cluster in the
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

| Parameter                                  | Description                                                                  | Default                          |
| ------------------------------------------ | ---------------------------------------------------------------------------- | -------------------------------- |
| agent.collectionInterval                   | Collection polling cycle for kubernetes datasource                           | `300s`                           |
| agent.logLevel                             | Log level for kubernetes datasource                                          | `debug`                          |
| `zenoss.clusterName`                       | Set a unique name for the Kubernetes cluster entity in Zenoss                | `nil`                            |
| `zenoss.name`                              | Arbitrary name for Zenoss endpoint to differentiate it from others           | `default`                        |
| `zenoss.address`                           | Zenoss API endpoint address: <name>:<port>                                   | `api.zenoss.io:443`              |
| `zenoss.apiKey`                            | Zenoss API key                                                               | `nil`                            |
| `zenoss.apiKeyExistingSecret`              | Existing Kubernetes secret containing Zenoss API key in `api-key` key        | `nil`                            |
| `zenoss.insecureTLS`                       | Allow insecure TLS connections to the zenoss endpoint                        | `false`                          |
| `zenoss.logUpdates`                        | Log all updates that are sent to zenoss                                      | `false`                          |
| `zenoss.useCompact`                        | Send compact metrics to zenoss                                               | `true`                           |
| `zenoss.endpoints[0].name`                 | Name for additional Zenoss endpoint                                          | `nil`                            |
| `zenoss.endpoints[0].address`              | Address for additional Zenoss endpoint: <name>:<port>                        | `api.zenoss.io:443`              |
| `zenoss.endpoints[0].apiKey`               | API key for additional Zenoss endpoint                                       | `nil`                            |
| `zenoss.endpoints[0].apiKeyExistingSecret` | Existing Kubernetes secret containing API key for additional Zenoss endpoint | `nil`                            |
| `zenoss.endpoints[0].insecureTLS`          | Allow insecure TLS connections to the zenoss endpoint                        | `false`                          |
| `zenoss.endpoints[0].logUpdates`           | Log all updates that are sent to zenoss                                      | `false`                          |
| `zenoss.endpoints[0].useCompact`           | Send compact metrics to zenoss                                               | `true`                           |
| `rbac.create`                              | Whether RBAC resources should be created                                     | `true`                           |
| `rbac.serviceAccountName`                  | Existing serviceAccountName to use if `rbac.create` is `false`               | `default`                        |
| `image.repository`                         | Image repository                                                             | `zenoss/zdatamon`                |
| `image.tag`                                | Image tag                                                                    | current version                  |
| `image.pullPolicy`                         | Image pull policy                                                            | `IfNotPresent`                   |
| `image.pullSecrets`                        | Docker registry secret names as an array                                     | `[]`                             |
| `resources`                                | CPU/Memory resource requests/limits                                          | `{}`                             |
| `nodeSelector`                             | Node labels for pod assignment                                               | `{}`                             |
| `tolerations`                              | Toleration labels for pod assignment                                         | `[]`                             |
| `affinity`                                 | Map of node/pod affinities                                                   | `{}`                             |
| `nameOverride`                             | String to partially override fullname template                               | `nil`                            |
| `fullnameOverride`                         | String to fully override fullname template                                   | `nil`                            |

Specify each parameter using the `--set key=value[,key=value]` argument to
`helm install`. For example:

```console
$ helm install \
    --name my-release \
    --set zenoss.clusterName=<K8S_CLUSTER_NAME> \
    --set zenoss.apiKey=<ZENOSS_API_KEY> \
    zenoss/zenoss-agent-kubernetes
```

The above command sets the minimum required parameters to install.

Alternatively, a YAML file that specifies the values for the parameters can be
provided while installing the chart. For example:

```console
$ helm install --name my-release -f values.yaml zenoss/zenoss-agent-kubernetes
```

[Helm]: https://helm.sh/
[Helm Quickstart Guide]: https://helm.sh/docs/using_helm/#quickstart
[Kubernetes]: https://kubernetes.io/
[Kubernetes Metrics Server]: https://github.com/kubernetes-incubator/metrics-server
[Zenoss]: https://www.zenoss.com/
[zenoss-agent-kubernetes]: https://github.com/zenoss/zenoss-agent-kubernetes
