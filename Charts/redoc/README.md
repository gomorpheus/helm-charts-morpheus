# Redoc
Redoc is an open-source tool for generating documentation from OpenAPI (fka Swagger) definitions.

This deploys the Redoc container found here: https://hub.docker.com/r/redocly/redoc/

## Deploying Redoc ##

**Configure Helm Repo**
```console
helm repo add morpheusdata https://gomorpheus.github.io/helm-charts-morpheus/
```
\
**Install Redoc**
Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
helm install redoc --set replicaCount="1" morpheusdata/redoc
```
Or supply a values YAML file and pass as an agrgument as follows:
```console
helm install -f values.yaml redoc morpheusdata/redoc
```

---
## Upgrading Redoc ##

There are no persistent items associated at this time.  Upgrading is simpling refreshing the repo and performing the following:

```console
helm repo update
helm upgrade -f values.yaml redoc morpheusdata/redoc
```

## Uninstalling Redoc Chart

To uninstall/delete deployment:
```console
helm uninstall redoc
```
or
```console
helm delete redoc --purge
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following tables lists the configurable parameters of the Sentry chart and their default values.

| Parameter                                   | Description                                                                                  | Default                                        |
| ------------------------------------------- | -------------------------------------------------------------------------------------------- | ---------------------------------------------- |
| `image.repository`                            | Image repository                                  | `morpheusdata/redoc`|
| `image.tag`                                   | Image tag. Possible values listed [here](https://hub.docker.com/r/redocly/redoc/tags). | `v2.0.0-rc.74`|
| `image.pullPolicy`                            | Image pull policy | `IfNotPresent`                |                           |
| `env.PAGE_TITLE`                              | Page Title                                        |  `<Optional>`             |
| `env.PAGE_FAVICON`                            | URL to page favicon                               |  `<Optional>`             |
| `env.SPEC_URL`                                | URL to spec                                       | `http://petstore.swagger.io/v2/swagger.json` |
| `env.PORT`                                    | nginx port                                        | `false`                   |
| `service.type`                                | Kubernetes service type for the GUI               | `ClusterIP`               |
| `service.port`                                | Kubernetes port where the GUI is exposed          | `8989`                    |
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