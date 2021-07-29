# Fury Kubernetes Kong

This repo contains Kong Ingress Controller for Kubernetes.

## Ingress Packages

Following packages are included in Fury Kubernetes Kong katalog:

### Open Source

- [kong-dbless](katalog/kong/kong-dbless): Default Kong Ingress, without DB. Ingress Version: **1.1.1**, Kong Version: **2.3.2**
- [kong-db](katalog/kong/kong-db): Kong Ingress that uses a postgres db for persistence. Ingress Version: **1.1.1**, Kong Version: **2.3.2**

### Enterprise

- [kong-enterprise](katalog/kong/kong-enterprise): The KONG Ingress Controller for Kubernetes with Kong Enterprise Edition.
  Version: Ingress: **1.1.1**, Kong Enterprise: **2.3.2.0**
- [kong-enterprise-hybrid](katalog/kong/kong-enterprise-hybrid): The KONG Ingress Controller for Kubernetes with Kong Enterprise Edition. Data Planes connected to Control Plane in Hybrid Mode.
  Version: Ingress: **1.1.1**, Kong Enterprise: **2.3.2.0**
- [kong-enterprise-k8s](katalog/kong/kong-enterprise-k8s): The KONG Ingress Controller for Kubernetes with Kong Enterprise Edition for K8s.
  Version: Ingress: **1.1.1**, Kong Enterprise: **2.3.2.0**



## Compatibility

| Module Version / Kubernetes Version | 1.14.X             | 1.15.X             | 1.16.X             | 1.17.X             | 1.18.X             | 1.19.X             |
|-------------------------------------|:------------------:|:------------------:|:------------------:|:------------------:|:------------------:|:------------------:|
| v1.0.0                              | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| v2.0.0                              |                    |                    |                    | :white_check_mark: | :white_check_mark: | :white_check_mark: |

- :white_check_mark: Compatible
- :warning: Has issues
- :x: Incompatible

