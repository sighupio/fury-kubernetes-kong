<h1>
    <img src="https://github.com/sighupio/fury-distribution/blob/main/docs/assets/fury-epta-white.png?raw=true" align="left" width="90" style="margin-right: 15px"/>
    Kubernetes Fury Kong
</h1>

![Release](https://img.shields.io/badge/Latest%20Release-v3.0.0-blue)
![License](https://img.shields.io/github/license/sighupio/fury-kubernetes-kong?label=License)
![Slack](https://img.shields.io/badge/slack-@kubernetes/fury-yellow.svg?logo=slack&label=Slack)

<!-- <KFD-DOCS> -->

**Kubernetes Fury Kong** contains Kong Ingress Controller for Kubernetes and all the possible deployment options as an
add-on for [Kubernetes Fury Distribution (KFD)][kfd-repo].

## Compatibility

| Kubernetes Version |   Compatibility    | Notes                                               |
|--------------------|:------------------:|-----------------------------------------------------|
| `1.21.x`           | :white_check_mark: | No known issues                                     |
| `1.22.x`           | :white_check_mark: | No known issues                                     |
| `1.23.x`           | :white_check_mark: | No known issues                                     |
| `1.24.x`           | :white_check_mark: | No known issues                                     |
| `1.25.x`           | :white_check_mark: | No known issues                                     |
| `1.26.x`           | :white_check_mark: | No known issues                                     |


Check the [compatibility matrix][compatibility-matrix] for additional information about previous releases of the modules.

### Open Source Packages

The following Open Source Packages packages are included in the Fury Kubernetes Kong add-on module:

| Package                                              | KIC Version  | Kong Version | Description                                           |
|------------------------------------------------------|--------------|--------------|-------------------------------------------------------|
| [kong-dbless](katalog/kong-dbless)              | `2.9.3`      | `3.2.2`      | Default Kong Ingress, without DB.                     |
| [kong-db](katalog/kong-db)                      | `2.9.3`      | `3.2.2`      | Kong Ingress that uses a postgres db for persistence  |


### Enterprise Packages

The following Enterprise packages are included in the Fury Kubernetes Kong add-on module:

| Package                                                        | KIC Version  | Kong Version | Description                                                                                                                      |
|----------------------------------------------------------------|--------------|--------------|----------------------------------------------------------------------------------------------------------------------------------|
| [kong-enterprise](katalog/kong-enterprise)                | `2.9.3`      | `3.2.2.1`    | The Kong Ingress Controller for Kubernetes with Kong Enterprise Edition.                                                         |
| [kong-enterprise-hybrid](katalog/kong-enterprise-hybrid)  | `2.9.3`      | `3.2.2.1`    | The Kong Ingress Controller for Kubernetes with Kong Enterprise Edition. Data Planes connected to Control Plane in Hybrid Mode.  |
| [kong-enterprise-k8s](katalog/kong-enterprise-k8s)        | `2.9.3`      | `3.2.2.1`    | The Kong Ingress Controller for Kubernetes with Kong Enterprise Edition for K8s.                                                 |

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
