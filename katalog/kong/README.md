# Kong ingress controller

Kong Ingress Controller is an Ingress Controller for [KONG](https://konghq.com/).


## Requirements

- Kubernetes >= `1.14.0`
- Kustomize >= `v3`


## Image repository and tag

* Kong image: `kong:2.0`
* Kong ingress controller image: `kong-docker-kubernetes-ingress-controller.bintray.io/kong-ingress-controller:0.8.1`


## Configuration

Fury distribution Kong is deployed with following configuration:

- Metrics are scraped by Prometheus every `10s`
- Service is configured as `NodePort` on ports:
    - 31081
    - 31444


## Deployment

You can deploy Kong ingress controller by running following command in the root of the project:

`$ kustomize build | kubectl apply -f -`


## Alerts

Followings Prometheus [alerts](https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/) are already defined for this package.

### ingress-kong.rules
| Parameter | Description | Severity | Interval |
|------|-------------|----------|:-----:|
| KongIngressDown | This alert fires if Prometheus target discovery was not able to reach kong ingress metrics in the last 15 minutes. | critical | 15m |


## License

For license details please see [LICENSE](../.../LICENSE)
