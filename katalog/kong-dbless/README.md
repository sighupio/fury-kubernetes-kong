# Kong DB-less

In this architecture, Kong Ingress Controller is deployed as sidecar with Kong Proxy.

Each Kong ingress controller reads the configuration from Kubernetes and writes the needed configurations inside Kong
Proxy.

