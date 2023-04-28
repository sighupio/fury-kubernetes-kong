# Kong DB

In this architecture, Kong Ingress Controller is deployed as sidecar with Kong Proxy.

Only one Ingress Controller at a time is the master, meaning that only one Ingress controller interacts with kong admin apis.
All the configurations are written by kong in the DB and all the other Kong Proxy will read the configurations from the DB.

## Prerequisites

| Tool                        | Version   | Description                                                                                                                                                    |
| --------------------------- | --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [furyctl][furyctl-repo]     | `>=0.6.0` | The recommended tool to download and manage KFD modules and their packages. To learn more about `furyctl` read the [official documentation][furyctl-repo].     |
| [kustomize][kustomize-repo] | `>=3.5.3` | Packages are customized using `kustomize`. To learn how to create your customization layer with `kustomize`, please refer to the [repository][kustomize-repo]. |

## Image repository and tag

* Kong image: `docker.io/library/kong:3.2.2`
* Kong ingress controller image: `docker.io/kong/kubernetes-ingress-controller:2.9.3`
* Postgres image: `docker.io/library/postgres:9.5`

## Configuration

- The environment variables as envFrom a secret instead of being env definition in the container
- A default podAntiAffinity on ingress-kong pods
- Service is exposed as `NodePort` with  `externalTrafficPolicy: Local` on ports:
  - `31081` for HTTP
  - `31444` for HTTPS
- Each pod is connected to a postgres db backend

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

4. Define a `kustomization.yaml` that includes the `./vendor/katalog/kong` directory as resource.

```yaml
resources:
  - ./vendor/katalog/kong-db
```

5. To deploy the packages to your cluster, execute:

```bash
kustomize build . | kubectl apply -f -
```

Eventually patch the number of replicas on your `kustomization.yaml` file with:

```yaml
resources:
  - ./vendor/katalog/kong-dbless

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
```

If you want to use an external DB create a new kong.env file and patch the postgres statefulset to put replicas to zero.

`kong.env`
```dotenv
KONG_PG_USER=youruser
KONG_PG_PASSWORD=yourpassword
KONG_PG_HOST=yourhost
KONG_PG_PORT=5432
```

Then on your `kustomization.yaml` file with:

```yaml
resources:
  - ./vendor/katalog/kong-dbless

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
  - |
    apiVersion: apps/v1
    kind: StatefulSet
    metadata:
      name: postgres
      namespace: kong
    spec:
      replicas: 0

secretGenerator:
  - name: kong-settings
    namespace: kong
    behavior: merge
    envs:
      - kong.env

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
