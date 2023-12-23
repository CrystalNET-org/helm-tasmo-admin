

<!-- markdownlint-disable MD033 -->

<h1 align="center">
    <a href="https://github.com/TasmoAdmin/TasmoAdmin">
        <img src="https://tasmota.github.io/docs/_media/logo.svg" alt="Logo" style="max-height: 150px">
    </a>
</h1>

<h4 align="center">Tasmo Admin - A Helm chart for TasmoAdmin - creates second ingress for http-only OTA server</h4>

<div align="center">
  <br/>

  [
    ![License](https://img.shields.io/github/license/zurdi15/romm?logo=git&logoColor=white&logoWidth=20)
  ](LICENSE)
  <br/>
  ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square)
  ![Version: 3.0.9](https://img.shields.io/badge/Version-3.0.9-informational?style=flat-square)
  ![AppVersion: v3.2.0](https://img.shields.io/badge/AppVersion-v3.2.0-informational?style=flat-square)
  [![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/CrystalNET)](https://artifacthub.io/packages/helm/crystalnet/paperless-ngx)

</div>

---

## [Tasmo Admin](https://github.com/TasmoAdmin/TasmoAdmin)

This is a helm chart for [TasmoAdmin](https://github.com/TasmoAdmin/TasmoAdmin)
it includes a second ingress (if you enable ingress) that serves the firmware updates via http
so you can access the frontend via https and just the updates are pushed via http

[> More about Tasmo Admin](https://github.com/TasmoAdmin/TasmoAdmin)

---

## TL;DR

Direct install via oci://:
```shell
helm install tasmo-admin oci://harbor.crystalnet.org/charts/tasmo-admin
```

install using chartMuseum:
```shell
helm repo add crystalnet https://charts.crystalnet.org
helm install tasmo-admin crystalnet/tasmo-admin
```

## Introduction

This chart bootstraps a Tasmo Admin deployment on a [Kubernetes](kubernetes.io) cluster using the [Helm](helm.sh) package manager.

## Prerequisites

- Helm 3+
- PV provisioner support in the underlying infrastructure

## Installing the Chart

To install the chart with the release name `my-release`:

Direct install via oci://:
```shell
helm install my-release oci://harbor.crystalnet.org/charts/tasmo-admin
```

install using chartMuseum:
```shell
helm repo add crystalnet https://charts.crystalnet.org
helm install my-release crystalnet/tasmo-admin
```

These commands deploy tasmo-admin on the Kubernetes cluster in the default configuration.
The Parameters section lists the parameters that can be configured during installation.

> **Tip:** List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```shell
helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Parameters

### Global parameters

| Key | Description | Default |
|-----|-------------|---------|

### Common parameters

| Key | Description | Default |
|-----|-------------|---------|
| `fullnameOverride` | String to fully override `common.names.fullname` template | `""` |
| `nameOverride` | String to partially override `common.names.fullname` template (will maintain the release name) | `""` |

### Tasmo Admin parameters

| Key | Description | Default |
|-----|-------------|---------|
| `image.pullPolicy` | pull policy, if you set tag to latest, this should be set to Always to not end up with stale builds | `"IfNotPresent"` |
| `image.repository` | referencing the docker image to use for the deployment | `"ghcr.io/tasmoadmin/tasmoadmin"` |
| `image.tag` | Overrides the image tag whose default is the chart appVersion. | `""` |
| `imagePullSecrets` | Reference to one or more secrets to be used when pulling images    ([kubernetes.io/docs](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/)) | `[]` |

### Security parameters

| Key | Description | Default |
|-----|-------------|---------|
| `podSecurityContext` |  | `{}` |
| `securityContext` |  | `{}` |

### Deployment/Statefulset parameters

| Key | Description | Default |
|-----|-------------|---------|
| `affinity` |  | `{}` |
| `nodeSelector` |  | `{}` |
| `podAnnotations` | If needed, set some annotations to the deployed pods | `{}` |
| `replicaCount` |  | `1` |
| `resources` | Limit the pods ressources if needed | `{}` |
| `tolerations` |  | `[]` |

### Network parameters

| Key | Description | Default |
|-----|-------------|---------|
| `ingress.annotations` | add annotations to the ingress object (for example to have certificates managed by cert-manager) | `{"nginx.ingress.kubernetes.io/proxy-body-size":"256m"}` |
| `ingress.className` | uses the default ingress class if not set | `""` |
| `ingress.enabled` | Enable creation of an ingress object for the deployment | `false` |
| `ingress.hosts[0]` | Hostname the ingress should react for | `{"host":"chart-example.local","paths":[{"path":"/","pathType":"ImplementationSpecific"}]}` |
| `ingress.tls` |  | `[]` |
| `service.port` |  | `80` |
| `service.type` | usually ClusterIP if you have an ingress in place,    could also be set to LoadBalancer if for example metallb is in place | `"ClusterIP"` |
| `serviceAccount.annotations` | Annotations to add to the service account | `{}` |
| `serviceAccount.create` | Specifies whether a service account should be created | `true` |
| `serviceAccount.name` | The name of the service account to use.    If not set and create is true, a name is generated using the fullname template | `""` |

### Persistence parameters

| Key | Description | Default |
|-----|-------------|---------|
| `persistence.accessMode` |  | `"ReadWriteOnce"` |
| `persistence.enabled` |  | `false` |
| `persistence.size` |  | `"20Mi"` |
| `persistence.storageClassName` |  | `""` |

### Database parameters

| Key | Description | Default |
|-----|-------------|---------|

### redis parameters

| Key | Description | Default |
|-----|-------------|---------|
### Other parameters

| Key | Description | Default |
|-----|-------------|---------|
| `autoscaling.enabled` |  | `false` |
| `autoscaling.maxReplicas` |  | `100` |
| `autoscaling.minReplicas` |  | `1` |
| `autoscaling.targetCPUUtilizationPercentage` |  | `80` |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```shell
helm install my-release --set fullnameOverride=my-tasmo-admin oci://harbor.crystalnet.org/charts/tasmo-admin
```

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```shell
helm install my-release -f values.yaml oci://harbor.crystalnet.org/charts/tasmo-admin
```

> **Tip:** You can use the default values.yaml

## License

Licensed under the GNU General Public License v3.0 (the "License"); you may not use this file except in compliance with
the License. You may obtain a copy of the License at

```
https://www.gnu.org/licenses/gpl-3.0.en.html
```

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific
language governing permissions and limitations under the License.

