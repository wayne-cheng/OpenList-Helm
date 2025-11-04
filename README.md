# OpenList Helm Chart

This chart bootstraps OpenList on [Kubernetes](http://kubernetes.io) using the [Helm](https://helm.sh) package manager.

## Prerequisites

- Kubernetes cluster 1.20+
- Helm v3.2.0+

## Configure OpenList Helm repo

```bash
helm repo add openlist https://openlistteam.github.io/OpenList-Helm
helm repo update
```

## Installing the Chart

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

| Parameter                  | Description                                                                 | Default                  |
|----------------------------|-----------------------------------------------------------------------------|--------------------------|
| `image.registry`           | Imag registry                                                               | `docker.io`              |
| `image.repository`         | Image name                                                                  | `openlistteam/openlist`  |
| `image.tag`                | Image tag                                                                   | `latest`                 |
| `image.pullPolicy`         | Image pull policy                                                           | `IfNotPresent`           |
| `persistence.storageClass` | Specify the storageClass used to provision the volume                       |                          |
| `persistence.accessMode`   | The access mode of the volume                                               | `ReadWriteOnce`          |
| `persistence.size`         | The size of the volume                                                      | `5Gi`                    |
| `service.type`             | Kubernetes service type                                                     | `ClusterIP`              |
| `service.loadBalancerIP`   | Kubernetes service loadBalancerIP                                           |                          |
| `service.http.port`        | Kubernetes service http port                                                | `5244`                   |
| `service.http.targetPort`  | Kubernetes service http targetPort                                          | `5244`                   |
| `service.http.nodePort`    | Kubernetes service http nodePort (valid only when `service.type=NodePort`)  | `35244`                  |
| `service.https.port`       | Kubernetes service https port                                               | `5245`                   |
| `service.https.targetPort` | Kubernetes service https targetPort                                         | `5245`                   |
| `service.https.nodePort`   | Kubernetes service https nodePort (valid only when `service.type=NodePort`) | `35245`                  |

If your Kubernetes cluster does not have a default StorageClass configured, please specify one explicitly.
For example:

```bash
helm install openlist openlist/openlist --namespace openlist --set persistence.storageClass=longhorn
```

## Uninstallation

To uninstall/delete the openlist deployment:

```bash
helm uninstall openlist --namespace openlist
kubectl delete namespace openlist
```

## Set the admin's password

You can **randomly generate** or **manually set**

```bash
# Randomly generate password
kubectl exec -n openlist $(kubectl get po -n openlist -l app=openlist | awk 'NR==2{print $1}') -- ./openlist admin random

# Manually set password to `NEW_PASSWORD` (replace this)
kubectl exec -n openlist $(kubectl get po -n openlist -l app=openlist | awk 'NR==2{print $1}') -- ./openlist admin set NEW_PASSWORD
```
