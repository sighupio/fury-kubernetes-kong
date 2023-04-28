# Kong enterprise Maintenance Guide

This package uses `kong-db` as base and adds on top some configurations.

What was added:

- Alerts for the CP (control-plane) component
- Settings divided in three secrets, one common, one for the CP and one for the DP
- Created kong-admin and kong-portal services as ClusterIP (they must be customized when Kong is installed)
- Kong Ingress controller is a sidecard for the CP and was removed from the DP
- Added a StatefulSet for the CP component
- Patched the validation service `kong-validation-webhook` to the CP instead of the DP