# OpenShift Upgrades

Stakater will perform one major OpenShift version upgrade per day per cluster.

Upgrades of test and staging clusters will typically be done first before production clusters.

The time it takes to upgrade the cluster depends on the number of nodes present on the cluster, typically ranging from 2 to 3 hours if no issues arise. However, in case any issues occur, the upgrade process may extend up to 6 hours.

The estimated times assume Stakater has cluster-admin access to the clusters.

Physical presence will only be required if any on-prem machines need to be restarted.

## Pre-Upgrade Steps

1. Run the following command on the cluster and share its output with Stakater:

    ```sh
    oc get apirequestcount
    ```

1. Verify all nodes are in the ready state
1. Confirm that all cluster operators are in the ready state
1. Check the health of PVs (Persistent Volumes) and PVCs (Persistent Volume Claims) to ensure:
    1. All PVs and PVCs are mounted
    1. None of the PVs and PVCs are unmounted
    1. None of the PVs and PVCs are stuck in the terminating state
    1. No abnormal configurations exist
1. Verify the health of machineConfigPools:
    1. Ensure `MACHINECOUNT` equals `READYMACHINECOUNT`
    1. Ensure there are no machines stuck in `UPDATEDMACHINECOUNT` or `DEGRADEDMACHINECOUNT`
1. Check the health of the etcd cluster
1. Confirm that no critical alerts exist on the cluster
1. The Customer needs to take a backup of the etcd cluster to ensure data safety in case of any issues during the upgrade process, see the official [`Backing up etcd` Red Hat documentation for the applicable version](https://docs.openshift.com/container-platform/4.15/backup_and_restore/control_plane_backup_and_restore/backing-up-etcd.html)

## Upgrade Steps

1. Start the upgrade from the cluster console
1. Monitor the upgrade process closely for any errors or warnings
1. If any error occurs or manual intervention is required, Stakater will address it promptly

## Post-Upgrade Steps

1. Perform all upgrade steps again to ensure the stability of the cluster
1. Verify that all nodes are in the ready state after the upgrade
1. Confirm that all cluster operators are functioning properly post-upgrade
1. Check the health of PVs and PVCs again to ensure successful migration and mounting
1. Verify the health of `machineConfigPools` and ensure the machine counts are as expected
1. Conduct tests or checks to ensure the etcd cluster is functioning correctly after the upgrade
1. Ensure all applications and services are running as expected on the upgraded cluster
1. Document any issues encountered during the upgrade process and their resolutions
1. Update the system documentation with details of the upgrade process, including any configurations or settings changed during the upgrade
1. Provide post-upgrade support to address any lingering issues or concerns
