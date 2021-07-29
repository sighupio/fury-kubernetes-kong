# Fury Kubernetes Kong

This repo contains Kong Ingress Controller for Kubernetes.

## Ingress Packages

Following packages are included in Fury Kubernetes Kong katalog:

- [kong](katalog/kong): The KONG Ingress Controller for Kubernetes
provides delivery API Gateway for Kubernetes applications. Version: **1.3.1**

## Compatibility

| Module Version / Kubernetes Version |       1.18.X       |       1.19.X       |       1.20.X       |  1.21.X   |
| ----------------------------------- | :----------------: | :----------------: | :----------------: | :-------: |
| v1.0.0                              |                    |                    |                    |           |
| v1.1.0                              | :white_check_mark: | :white_check_mark: | :white_check_mark: | :warning: |
| v2.0.0                              | :white_check_mark: | :white_check_mark: | :white_check_mark: | :warning: |

### Open Source

- [kong-dbless](katalog/kong/kong-dbless): Default Kong Ingress, without DB. Ingress Version: **1.3.1**, Kong Version: **2.3.2**
- [kong-db](katalog/kong/kong-db): Kong Ingress that uses a postgres db for persistence. Ingress Version: **1.3.1**, Kong Version: **2.3.2**

### Enterprise

- [kong-enterprise](katalog/kong/kong-enterprise): The KONG Ingress Controller for Kubernetes with Kong Enterprise Edition.
  Version: Ingress: **1.3.1**, Kong Enterprise: **2.4.1.1**
- [kong-enterprise-hybrid](katalog/kong/kong-enterprise-hybrid): The KONG Ingress Controller for Kubernetes with Kong Enterprise Edition. Data Planes connected to Control Plane in Hybrid Mode.
  Version: Ingress: **1.3.1**, Kong Enterprise: **2.4.1.1**
- [kong-enterprise-k8s](katalog/kong/kong-enterprise-k8s): The KONG Ingress Controller for Kubernetes with Kong Enterprise Edition for K8s.
  Version: Ingress: **1.3.1**, Kong Enterprise: **2.4.1.1**

## License

For license details, please see [LICENSE](LICENSE)
