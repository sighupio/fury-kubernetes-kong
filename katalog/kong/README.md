# Kong ingress controller

Kong Ingress Controller is an Ingress Controller for [KONG](https://konghq.com/).
In these manifests folder we put all the needed manifests to deploy all sorts of kong architectures:

* `base` contains only the common resources used by ALL the deployment types
* `postgres` contains only the resources to deploy the postgresql pod (needed by other type of deployment)
* [Architecture Info](kong-dbless/README.md) `kong-dbless` is the kong ingress controller open source without DB
* [Architecture Info](kong-db/README.md) `kong-db` is the kong ingress controller plus DB
* [Architecture Info](kong-enterprise-k8s/README.md) `kong-enterprise-k8s` is the kong ingress controller without DB but with the enterprise image
* [Architecture Info](kong-enterprise/README.md) `kong-enterprise` This folder contains the Kong Enterprise deployment. We split control plane and data plane. 
The control plane part is a statefulset and the data plane part is a daemonset. 
Only the statefulset contains the kong ingress as a sidecar.
* [Architecture Info](kong-enterprise-hybrid/README.md) `kong-enterprise-hybrid` this folders extends the `kong-enterprise` adding the services needed to intercommunicate 
between control plane and data plane and adds the secret generation for the TLS used for the internal communication of kong.


## Requirements

- Kubernetes >= `1.14.0`
- Kustomize >= `v3`


## Image repository and tag

* Kong image: `kong:2.1`
* Kong ingress controller image: `kong-docker-kubernetes-ingress-controller.bintray.io/kong-ingress-controller:0.10.0`
* Kong Ingress Enterprise for K8s: `kong-docker-kong-enterprise-k8s.bintray.io/kong-enterprise-k8s:2.0.4.2-alpine`
* Kong Enterprise: `kong-docker-kong-enterprise-edition-docker.bintray.io/kong-enterprise-edition:2.3.2.0-alpine`

## Configuration

Fury distribution Kong is deployed with following configuration:

- Metrics are scraped by Prometheus every `10s`
- Kong ingress controller is a DaemonSet and not a Deployment
- Service is exposed as `NodePort` on ports:
    - `31081` for HTTP
    - `31444` for HTTPS
- Set `externalTrafficPolicy: Local` on kong service
- There are two different servicemonitors for the Enterprise CP/DP architecture, one for the CP and one for DP.


## Deployment

You can deploy Kong ingress controller by running following command in the selected architecture folder, remember to put your real secrets (or patch them):

`$ kustomize build | kubectl apply -f -`

## Alerts

Followings Prometheus [alerts](https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/) are already defined for this package.

### ingress-kong.rules
| Parameter | Description | Severity | Interval |
|------|-------------|----------|:-----:|
| KongIngressDown | This alert fires if Prometheus target discovery was not able to reach kong ingress metrics in the last 15 minutes. | critical | 15m |
| KongCPIngressDown | This alert fires if Prometheus target discovery was not able to reach kong control plane metrics in the last 15 minutes. (only on enterprise) | critical | 15m |

## License

For license details please see [LICENSE](../../LICENSE)
