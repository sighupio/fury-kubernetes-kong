# Kong DB architecture

In this architecture, Kong Ingress Controller is deployed as sidecar with Kong Proxy. 

Only one Ingress Controller at a time is
the master, meaning that only one Ingress controller interacts with kong admin apis. All the configurations are written by kong
in the DB and all the other Kong Proxy will read the configurations from the DB.

This is a turnkey solution, you can eventually change some configuration like the service that is exposing the 
kong ingress in the cluster and some fine tuning in the kong gateway. You can also put the statefulset we bundle in the deployment at 0 and change
the addresses of your database of choice.