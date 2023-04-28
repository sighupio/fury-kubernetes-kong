# Base Kong Maintenance Guide

To maintain the base package, you should follow these steps.

First of all, download the manifests from the [Kong/kubernetes-ingress-controller]() repository, for example from
https://github.com/Kong/kubernetes-ingress-controller/blob/v2.9.3/deploy/single/all-in-one-dbless-legacy.yaml .

Check the differences between [upstream/all-in-one-dbless-legacy.yaml](upstream/all-in-one-dbless-legacy.yaml) file.

Verify that the patching layer we are doing is still valid. 

What we are customizing:

- Adding the official grafana dashboard as a configmap
- Adding some basic alerts to check if Kong is down
- Adding the Prometheus ServiceMonitor to monitor data-planes
- Setting the environment variables as envFrom a secret instead of being env definition in the container
- Applying a default podAntiAffinity
