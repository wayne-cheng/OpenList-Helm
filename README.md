# OpenList Helm Chart

This chart bootstraps OpenList on [Kubernetes](http://kubernetes.io) using the [Helm](https://helm.sh) package manager.

## Prerequisites

- Kubernetes cluster 1.20+
- Helm v3.2.0+

## Configure OpenList Helm repo

```bash
helm repo add openlist https://wayne-cheng.github.io/OpenList-Helm
helm repo update
```

### Installing the Chart

Create the namespace `openlist`.

```bash
kubectl create namespace openlist
```

Install the helm chart into the namespace `openlist`.

```bash
helm install openlist openlist/openlist --namespace openlist
```

### Values reference

The default values.yaml should be suitable for most basic deployments.

| Parameter                  | Description                                                  | Default                         |
|----------------------------|--------------------------------------------------------------|---------------------------------|
| `image.registry`           | Imag registry                                                | `docker.io`                     |
| `image.repository`         | Image name                                                   | `openlistteam/openlist`         |
| `image.tag`                | Image tag                                                    | `latest`                        |
| `image.pullPolicy`         | Image pull policy                                            | `IfNotPresent`                  |
| `replicaCount`             | Number of scanner adapter Pods to run                        | `1`                             |
| `persistence.storageClass` | Specify the storageClass used to provision the volume        |                                 |
| `persistence.accessMode`   | The access mode of the volume                                | `ReadWriteOnce`                 |
| `persistence.size`         | The size of the volume                                       | `5Gi`                           |
| `service.type`             | Kubernetes service type                                      | `ClusterIP`                     |
| `service.loadBalancerIP`   | Kubernetes service loadBalancerIP                            |                                 |
| `service.http.port`        | Kubernetes service http port                                 | `5244`                          |
| `service.http.targetPort`  | Kubernetes service http targetPort                           | `5244`                          |
| `service.http.nodePort`    | Kubernetes service http nodePort                             | `35244`                         |
| `service.https.port`       | Kubernetes service https port                                | `5245`                          |
| `service.https.targetPort` | Kubernetes service https targetPort                          | `5245`                          |
| `service.https.nodePort`   | Kubernetes service https nodePort                            | `35245`                         |

If your Kubernetes cluster does not have a default StorageClass configured, please specify one explicitly.
For example:

```shell
helm install openlist openlist/openlist --namespace openlist --set persistence.storageClass=longhorn
```
