# Kong DB

In this architecture, Kong Ingress Controller is deployed as sidecar with Kong Proxy.

Only one Ingress Controller at a time is the master, meaning that only one Ingress controller interacts with kong admin apis.
All the configurations are written by kong in the DB and all the other Kong Proxy will read the configurations from the DB.


