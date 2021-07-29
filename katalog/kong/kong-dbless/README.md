# Kong DB-less architecture

In this architecture, Kong Ingress Controller is deployed as sidecar with Kong Proxy.

Each Kong ingress controller reads the configuration from Kubernetes and writes the needed configurations inside Kong
Proxy.

This deployment is a turnkey solution, you can eventually change some configurations like the service that is exposing
the kong ingress in the cluster and some fine-tuning in the kong gateway.
