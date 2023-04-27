# Kong Enterprise Hybrid

In this architecture, we have two components, the Data Plane and the Control Plane. All the images we are using for
Kong are the Enterprise Images.

The Kong Ingress controller is deployed in the Control Plane statefulset as a Sidecar.

The Kong Data Plane is deployed as a Deployment, all the Kong Data Plane reads the configurations from the Control Plane
directly with a TLS connection.

![Kong Enterprise Hybrid Architecture](../../docs/images/deployment-hybrid-2.png)



