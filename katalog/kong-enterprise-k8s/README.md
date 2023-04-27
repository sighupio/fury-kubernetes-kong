# Kong DB-less Enterprise

In this architecture, Kong Ingress Controller is deployed as sidecar with Kong Proxy.

Each Kong ingress controller reads the configuration from Kubernetes and writes the needed configurations inside
Kong Proxy.

The Kong Proxy is the Enterprise one, meaning that you can also deploy Enterprise plugins on your kong configurations.

