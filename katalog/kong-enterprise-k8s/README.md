# Kong DB-less Enterprise

In this architecture, Kong Ingress Controller is deployed as sidecar with Kong Proxy.

Each Kong ingress controller reads the configuration from Kubernetes and writes the needed configurations inside
Kong Proxy.

The Kong Proxy is the Enterprise one, meaning that you can also deploy Enterprise plugins on your kong configurations.

## Prerequisites

| Tool                        | Version   | Description                                                                                                                                                    |
| --------------------------- | --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [furyctl][furyctl-repo]     | `>=0.6.0` | The recommended tool to download and manage KFD modules and their packages. To learn more about `furyctl` read the [official documentation][furyctl-repo].     |
| [kustomize][kustomize-repo] | `>=3.5.3` | Packages are customized using `kustomize`. To learn how to create your customization layer with `kustomize`, please refer to the [repository][kustomize-repo]. |

## Image repository and tag

* Kong image: `docker.io/library/kong:3.2.2`
* Kong ingress controller image: `docker.io/kong/kubernetes-ingress-controller:2.9.3`

## Configuration

- The environment variables as envFrom a secret instead of being env definition in the container
- A default podAntiAffinity on ingress-kong pods
- Service is exposed as `NodePort` with  `externalTrafficPolicy: Local` on ports:
  - `31081` for HTTP
  - `31444` for HTTPS

## Deployment

> Note :warning:: in this example we are showing only basic configurations

1. List the packages you want to deploy and their version in a `Furyfile.yml`

```yaml
bases:
  - name: kong
```

> See `furyctl` [documentation][furyctl-repo] for additional details about `Furyfile.yml` format.

2. Execute `furyctl vendor -H` to download the packages

3. Inspect the download packages under `./vendor/katalog/kong`.

4. To deploy a working kong enterprise you need to define a `kustomization.yaml` file and patch the following :

```yaml
resources:
  - ./vendor/katalog/kong-enterprise-k8s

patchesStrategicMerge:
  - |
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      labels:
        app: ingress-kong
      name: ingress-kong
      namespace: kong
    spec:
      replicas: 3

secretGenerator:
  - name: kong-enterprise-license
    behaviour: replace
    namespace: kong
    files:
      - license=secrets/license.json
```

## Alerts

Followings Prometheus [alerts](https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/) are already defined for this package.

### ingress-kong.rules

| Parameter | Description | Severity | Interval |
|------|-------------|----------|:-----:|
| KongIngressDown | This alert fires if Prometheus target discovery was not able to reach kong ingress metrics in the last 15 minutes. | critical | 15m |`

<!-- Links -->

[furyctl-repo]: https://github.com/sighupio/furyctl
[kustomize-repo]: https://github.com/kubernetes-sigs/kustomize