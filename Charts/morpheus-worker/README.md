# Morpheus Worker

## Deploying Morpheus Worker Nodes ##

**Configure Helm Repo**
```console
helm repo add morpheusdata https://gomorpheus.github.io/helm-charts-morpheus/
```
\
**Install Morpheus Worker**
Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
helm install morpheus-worker --set replicaCount="1" morpheusdata/morpheus-worker
```
Or supply a values YAML file and pass as an agrgument as follows:
```console
helm install -f values.yaml morpheus-worker morpheusdata/morpheus-worker
```

---
## Upgrading Morpheus Worker Nodes ##

There are no persistent items associated with Worker Nodes at this time.  Upgrading is simpling refreshing the repo and performing the following:

```console
helm repo update
helm upgrade -f values.yaml morpheus-worker morpheusdata/morpheus-worker
```

## Uninstalling Morpheus Worker Chart

To uninstall/delete deployment:
```console
helm uninstall morpheus-worker
```
or
```console
helm delete morpheus-worker --purge
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following tables lists the configurable parameters of the Sentry chart and their default values.

| Parameter                                   | Description                                                                                  | Default                                        |
| ------------------------------------------- | -------------------------------------------------------------------------------------------- | ---------------------------------------------- |
| `image.repository`                            | Image repository                                  | `morpheusdata/morpheus-worker`|
| `image.tag`                                   | Image tag. Possible values listed [here](https://hub.docker.com/r/morpheusdata/morpheus-worker/tags). | `5.3.1-4`|
| `image.pullPolicy`                            | Image pull policy | `IfNotPresent`                |                           |
| `env.MORPHEUS_KEY`                            | API Key for Morpheus Worker                       |                           |
| `env.MORPHEUS_URL`                            | Morpheus FQDN with protocol                       |                           |
| `env.MORPHEUS_SELF_SIGNED`                    | Is Morpheus using a Self Signed Certificate       | `false`                   |
| `service.type`                                | Kubernetes service type for the GUI               | `ClusterIP`               |
| `service.port`                                | Kubernetes port where the GUI is exposed          | `8989`                    |
| `livenessProbe.initialDelaySeconds`           | Initial delay (seconds) for liveness monitoring   | `5`                       |
| `livenessProbe.timeoutSeconds`                | Timeout (seconds) before health check considered unhealthy | `5`              |
| `livenessProbe.periodSeconds`                 | Poll interval (seconds) between health checks     | `10`                      |
| `livenessProbe.failureThreshold`              | Number of failed polls before restarting service  | `3`                       |
| `replicaCount`                                | Number of Replicas if AutoScaling False           | `1`                       |
| `autoscaling.enabled`                         | Enable AutoScaling                                | `false`                   |
| `autoscaling.minReplicas`                     | Minimum number of Replicas                        | `1`                       |
| `autoscaling.maxReplicas`                     | Maximum number of Replicas                        | `100`                     |
| `autoscaling.targetCPUUtilizationPercentage`  | CPU Threshold for AutoScaling                     | `80`                      |
| `autoscaling.targetMemoryUtilizationPercentage`| Memory Threshold for AutoScaling                 | `80`                      |
| `ingress.enabled`                             | Enables Ingress                                   | `false`                   |
| `ingress.annotations`                         | Ingress annotations                               | `{}`                      |
| `ingress.path`                                | Ingress path                                      | `/`                       |
| `ingress.hosts`                               | Ingress accepted hostnames                        | `chart-example.local`     |
| `ingress.tls`                                 | Ingress TLS configuration                         | `[]`                      |
| `resources`                                   | CPU/Memory resource requests/limits               | `{}`                      |
| `nodeSelector`                                | Node labels for pod assignment                    | `{}`                      |
| `tolerations`                                 | Toleration labels for pod assignment              | `[]`                      |
| `affinity`                                    | Affinity settings for pod assignment              | `{}`                      |

---