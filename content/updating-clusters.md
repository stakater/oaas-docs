# Updating Clusters

`Version: 30 Jan 2023`

The OpenShift cluster and its components are constantly evolving, with functional and security issues being detected and fixed during operation. New features emerge regularly.

## Types of Updates

The following update types are available:

* Major-release is a planned update of cluster components that involves making backwards-incompatible API changes. Releases result in incrementing the major version (`X`) component in the semantic version number (`X.Y.Z`).

* Minor-release is a planned update of cluster components that involves a feature extension or change. Releases result in incrementing the minor version (`Y`) component in the semantic version number (`X.Y.Z`).

* Patch-release is an unplanned update of cluster components to fix errors or other functional issues that have already led or may lead to instability of the cluster. Patch-releases result in incrementing the patch version (`Z`) component in the semantic version number (`X.Y.Z`).

The cluster may be updated on a schedule according to the update windows defined for the cluster. The available options for configuring update windows for the cluster are:

Type of update | Update time | Non-Prod | Prod
--- | --- | --- | ---
Major- or Minor-release | Regular business hours | Selecting a time window for updates isn't possible | Selecting a time window for updates is possible
Major- or Minor-release | Non-business hours | Not available | For an additional fee
Patch-release | Regular business hours | Selecting a time window for updates isn't possible | Selecting a time window for updates isn't possible
Patch-release | Non-business hours | Not available | For an additional fee
