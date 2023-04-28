# Base Kong

This package should not be directly used, use the `kong-*` packages instead. It still needs to be imported because is used as
a base for the other packages.

In this package we are applying some customization from the upstream manifests:

- Adding the official grafana dashboard as a configmap
- Adding some basic alerts to check if Kong is down
- Adding the Prometheus ServiceMonitor to monitor data-planes
- Setting the environment variables as envFrom a secret instead of being env definition in the container
- Applying a default podAntiAffinity
- Service is exposed as `NodePort` on ports:
  - `31081` for HTTP
  - `31444` for HTTPS
- Set `externalTrafficPolicy: Local` on kong service

See [MAINTENANCE.md](MAINTENANCE.md) to know how to maintain the package.

## Alerts

Followings Prometheus [alerts](https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/) are already defined for this package.

### ingress-kong.rules

| Parameter | Description | Severity | Interval |
|------|-------------|----------|:-----:|
| KongIngressDown | This alert fires if Prometheus target discovery was not able to reach kong ingress metrics in the last 15 minutes. | critical | 15m |
