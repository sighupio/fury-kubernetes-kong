# Kong Enterprise Hybrid architecture

In this architecture, we have two components, the Data Plane and the Control Plane. All the images we are using for Kong are the
Enterprise Images.

The Kong Ingress controller is deployed in the Control Plane statefulset as a Sidecar.

The Kong Data Plane is deployed as a daemonset, all the Kong Data Plane reads the configurations from the Control Plane 
directly with a TLS connection.

![Kong Enterprise Hybrid Architecture](../../../docs/images/deployment-hybrid-2.png)

This deployment is a turnkey solution, you can eventually change some configuration like the service that is exposing the 
kong ingress in the cluster and some fine tuning in the kong gateway. You will need to add the correct `secrets` like the
license and the .dockerconfigjson credentials needed to download the docker image and also **IMPORTANT** change the TLS certificate.
Use the bundled script `cluster-tls/generate.sh` to regenerate them.

There are also three more service exposed, one for the Kong Manager and Kong Admin API and one for the Developer Portal and Developer
Portal API, one more is an internal service for the intra communication between Kong CP and Kong DP.
