<h1>
    <img src="https://github.com/sighupio/fury-distribution/blob/master/docs/assets/fury-epta-white.png?raw=true" align="left" width="90" style="margin-right: 15px"/>
    Kubernetes Fury Kong
</h1>

![Release](https://img.shields.io/badge/Latest%20Release-v2.8.1-blue)
![License](https://img.shields.io/github/license/sighupio/fury-kubernetes-kong?label=License)
![Slack](https://img.shields.io/badge/slack-@kubernetes/fury-yellow.svg?logo=slack&label=Slack)

<!-- <KFD-DOCS> -->

*Kubernetes Fury Kong* contains Kong Ingress Controller for Kubernetes and all the possible deployment options as an
add-on for [Kubernetes Fury Distribution (KFD)][kfd-repo].

## Compatibility

| Kubernetes Version |   Compatibility    | Notes                                               |
|--------------------|:------------------:|-----------------------------------------------------|
| `1.20.x`           | :white_check_mark: | No known issues                                     |
| `1.21.x`           | :white_check_mark: | No known issues                                     |
| `1.22.x`           | :white_check_mark: | No known issues                                     |
| `1.23.x`           | :white_check_mark: | No known issues                                     |

Check the [compatibility matrix][compatibility-matrix] for additional information about previous releases of the modules.

### Open Source Packages

- [kong-dbless](katalog/kong/kong-dbless): Default Kong Ingress, without DB. Ingress Version: **2.3.1**, Kong Version: **2.8.1**
- [kong-db](katalog/kong/kong-db): Kong Ingress that uses a postgres db for persistence. Ingress Version: **2.3.1**, Kong Version: **2.8.1**

### Enterprise Packages

- [kong-enterprise](katalog/kong/kong-enterprise): The KONG Ingress Controller for Kubernetes with Kong Enterprise Edition.
  Version: Ingress: **2.3.1**, Kong Enterprise: **2.8.1.0**
- [kong-enterprise-hybrid](katalog/kong/kong-enterprise-hybrid): The KONG Ingress Controller for Kubernetes with Kong Enterprise Edition. Data Planes connected to Control Plane in Hybrid Mode.
  Version: Ingress: **2.3.1**, Kong Enterprise: **2.8.1.0**
- [kong-enterprise-k8s](katalog/kong/kong-enterprise-k8s): The KONG Ingress Controller for Kubernetes with Kong Enterprise Edition for K8s.
  Version: Ingress: **2.3.1**, Kong Enterprise: **2.8.1.0**

<!-- Links -->

[kfd-repo]: https://github.com/sighupio/fury-distribution
[kfd-docs]: https://docs.kubernetesfury.com/docs/distribution/
[compatibility-matrix]: https://github.com/sighupio/fury-kubernetes-kong/blob/master/docs/COMPATIBILITY_MATRIX.md

<!-- </KFD-DOCS> -->

<!-- <FOOTER> -->

## Contributing

Before contributing, please read first the [Contributing Guidelines](docs/CONTRIBUTING.md).

### Reporting Issues

In case you experience any problem with the module, please [open a new issue](https://github.com/sighupio/fury-kubernetes-kong/issues/new/choose).

## License

This module is open-source and it's released under the following [LICENSE](LICENSE)

<!-- </FOOTER> -->
