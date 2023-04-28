# Kong Enterprise Hybrid

In this architecture, we have two components, the Data Plane and the Control Plane. All the images we are using for
Kong are the Enterprise Images.

The Kong Ingress controller is deployed in the Control Plane statefulset as a Sidecar.

The Kong Data Plane is deployed as a Deployment, all the Kong Data Plane reads the configurations from the Control Plane
directly with a TLS connection.

![Kong Enterprise Hybrid Architecture](../../docs/images/deployment-hybrid-2.png)

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
- data planes are connected to the control plane with mTLS
- There are three secrets used to configure kong:
  - `kong-settings` common configurations for all the components, control plane and data plane
  - `kong-settings-cp` dedicated configurations for control planes
  - `kong-settings-dp` dedicated configurations for data planes
- A default podAntiAffinity on ingress-kong pods
- Additional serviceMonitor for the control plane component
- `kong-proxy` Service is exposed as `NodePort` with  `externalTrafficPolicy: Local` on NodePorts:
  - `31081` for HTTP
  - `31444` for HTTPS
- `kong-portal` and `kong-admin` services are not exposed by default

## Deployment

> Note :warning:: in this example we are showing some of the configurations that should be used in a EKS cluster with the ALB controller installed, and these are not full production grade settings.

1. List the packages you want to deploy and their version in a `Furyfile.yml`

```yaml
bases:
  - name: kong
```

> See `furyctl` [documentation][furyctl-repo] for additional details about `Furyfile.yml` format.

2. Execute `furyctl vendor -H` to download the packages

3. Inspect the download packages under `./vendor/katalog/kong`.

4. Generate a cluster.key and a cluster.crt file to establish mTLS between CP and DP

```bash
openssl req -new -x509 -nodes -newkey ec:<(openssl ecparam -name secp384r1) \
  -keyout cluster.key -out cluster.crt \
  -days 1095 -subj "/CN=kong_clustering"
```

5. To deploy a working kong enterprise you need to patch the following :

```yaml
resources:
  - ./vendor/katalog/kong-enteprise

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
    apiVersion: v1
    kind: Service
    metadata:
      annotations:
        service.beta.kubernetes.io/aws-load-balancer-scheme: internet-facing
        service.beta.kubernetes.io/aws-load-balancer-type: "external"
        service.beta.kubernetes.io/aws-load-balancer-nlb-target-type: "instance"
      name: kong-proxy
      namespace: kong
    spec:
      type: LoadBalancer
  - |
    apiVersion: v1
    kind: Service
    metadata:
      annotations:
        service.beta.kubernetes.io/aws-load-balancer-type: "external"
        service.beta.kubernetes.io/aws-load-balancer-nlb-target-type: "instance"
      name: kong-admin
      namespace: kong
    spec:
      type: LoadBalancer
  - |
    apiVersion: v1
    kind: Service
    metadata:
      annotations:
        service.beta.kubernetes.io/aws-load-balancer-scheme: internet-facing
        service.beta.kubernetes.io/aws-load-balancer-type: "external"
        service.beta.kubernetes.io/aws-load-balancer-nlb-target-type: "instance"
      name: kong-portal
      namespace: kong
    spec:
      type: LoadBalancer
  

secretGenerator:
  - name: kong-settings
    behavior: merge
    namespace: kong
    envs:
      - kong-common.env
  - name: kong-settings-cp
    behaviour: merge
    namespace: kong
    envs:
      - kong-cp.env
  - name: kong-enterprise-license
    behaviour: replace
    namespace: kong
    files:
      - license=secrets/license.json
  - name: kong-cluster-cert
    behaviour: replace
    namespace: kong
    type: kubernetes.io/tls
    files:
      - tls.crt=cluster.crt
      - tls.key=cluster.key
```

`kong-common.env`
```dotenv
KONG_PORTAL_GUI_HOST=developer.example.com
KONG_PORTAL_API_URL=http://developer.example.com:8080
```

`kong-cp.env`
```dotenv
KONG_ADMIN_API_URI=http://manager.example.com:8080
KONG_ADMIN_GUI_URL=http://manager.example.com
```

6. To deploy the packages to your cluster, execute:

```bash
kustomize build . | kubectl apply -f -
```

## Alerts

Followings Prometheus [alerts](https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/) are already defined for this package.

### ingress-kong.rules
| Parameter | Description | Severity | Interval |
|------|-------------|----------|:-----:|
| KongIngressDown | This alert fires if Prometheus target discovery was not able to reach kong ingress metrics in the last 15 minutes. | critical | 15m |
| KongCPIngressDown | This alert fires if Prometheus target discovery was not able to reach kong control plane metrics in the last 15 minutes. (only on enterprise) | critical | 15m |

<!-- Links -->

[furyctl-repo]: https://github.com/sighupio/furyctl
[kustomize-repo]: https://github.com/kubernetes-sigs/kustomize