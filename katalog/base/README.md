# Base Kong

This package should not be directly used, use the `kong-*` packages instead. It still needs to be imported because is used as
a base for the other packages.

In this package we are applying some customization from the upstream manifests:

- Adding the official grafana dashboard as a configmap
- Adding some basic alerts to check if Kong is down
- Adding the Prometheus ServiceMonitor to monitor data-planes
- Setting the environment variables as envFrom a secret instead of being env definition in the container
- Applying a default podAntiAffinity

See [MAINTENANCE.md](MAINTENANCE.md) to know how to maintain the package.