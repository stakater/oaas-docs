# Service Level Agreement (SLA)

`Version: 30 Jan 2023`

This SLA establishes conditions and a method for measuring the level of service at a given time, defines the guaranteed level of service, and sets out penalties for violating the guaranteed level of service.

The level of service is measured based on monitoring data for individual cluster components grouped into availability types. Some availability types require enabling a special high availability mode of operation of components of the OpenShift cluster (elsewhere referred to as the High Availability mode, HA) to ensure a guaranteed level of service.

Specifications and operating conditions of components running in the High Availability mode:

* The component is run in two or more instances to preserve availability in the case of a failure of a single instance
* Enabling this mode requires additional computing resources
* If there is more than one master node in the cluster, the High Availability mode is activated for all components by default
* The HA mode can be turned off for individual components, such as authentication and monitoring, to reduce the cost of computing resources. However, we cannot guarantee the Service Level (SL) for such subsystems.
* Control Plane — the cluster core — is considered running in the HA mode if it has at least three instances

## Availability Types

To accurately identify types of degradations and the degree of their impact on the performance of services, we define several types of unavailability for which it is possible to set the parameters under the SLA.

### Synthetic Availability

Synthetic availability is the availability of running applications in the cluster and cluster components that are not related to the availability of the cluster's Control Plane.

The SLA for Synthetic Availability is valid only if these basic conditions are met:

* Cluster nodes continue to be available
* There is network connectivity between nodes
* The application continues to operate correctly

At the same time, applications keep on running that meet the following conditions:

* The application itself caches DNS data
* The application can operate with no scheduler or autoscaler running as well as with no ability to add/edit service endpoints
* No `kube-apiserver` availability is required for the application to operate

This availability type does not require enabling the HA mode for components.

### Router Availability

Router availability is the availability of ingress router and its components - incoming HTTP requests are delivered to end applications.

The router availability SLA does not cover the network availability that depends on the infrastructure.

This availability type requires enabling the HA mode for components.

### Node Group Availability

In managed OpenShift, nodes are grouped together based on a purpose and managed as an integrated entity. All nodes in the group have the same metadata defined in the parameters of a `NodeGroup` resource based on labels, annotations, or taint fields. Such a group of nodes is called the Node Group.

Node Group Availability indicates that each Node Group has at least `N-1` correctly functioning nodes, where `N` is the minimum number of nodes in NodeGroup as defined in the configuration.

The Node Group Availability SLA does not apply to cases when a node fails due to improper operation of an application installed by the customer.

This availability type does not require enabling the HA mode for components.

### Control Plane Availability

Control plane availability indicates that the deployment process in the cluster is working, and self-healing processes are running. It formulates the availability level of the main control OpenShift components:

* `console`
* `etcd`
* `ingress`
* `kube-apiserver`
* `kube-controller-manager`
* `kube-dns`
* `kube-scheduler`
* `oauth-server`
* `openshift-apiserver`
* `openshift-cluster-csi-drivers`
* `openshift-cluster-node-tuning-operator`
* `openshift-image-registry`
* `openshift-kube-scheduler`
* `openshift-multus`
* `openshift-operator-lifecycle-manager`
* `openshift-sdn`
* `openshift-storage-operator`
* other components that the API depends on, such as Vertical Pod Autoscaler's admission controller

This availability type requires enabling the HA mode for components.

### Monitoring and Autoscaling Availability

Monitoring and autoscaling availability means that monitoring and autoscaling are operating correctly. It defines the Prometheus availability level and auto scaling capabilities of components and data sources:

* Prometheus
* Vertical Pod Autoscaler
* Horizontal Pod Autoscaler

This availability type requires enabling the HA mode for components.

### Extensions Availability

Extensions availability means that additional Kubernetes components could be available. It sets out the availability level of components not directly involved in delivering applications to the runtime environment and their operation in the cluster, such as addons from Stakater listed on [Managed AddOns](../sre/addons/introduction.md).

This availability type requires enabling the HA mode for components.

### Common SLA Conditions for all Availability Types

Availability types do not apply to situations of complete lack of network connectivity between nodes or total inaccessibility of the cluster infrastructure.

The availability of each cluster component individually and of the availability type as a whole is determined by the best value obtained from multiple probing agents.

## Guaranteed Level of Service

Availability Type | Non-Prod | Prod
--- | --- | ---
Synthetic | 99.0% | 99.5%
Router | 99.0% | 99.5%
Node Group | 99.0% | 99.5%
Control Plane | 99.0% | 99.5%
Monitoring and Autoscaling | 99.0% | 99.5%
Extensions | 99.0% | 99.5%

## Penalties for Violating the Service Level

Stakater shall pay the penalty at the Customer's request for violation of the SLA conditions. The amount of the penalty is determined as follows:

Penalty | Non-Prod | Prod
--- | --- | ---
The maximum amount of penalty per month of service for violating the SLA | No more than 10% of the monthly cost of service | No more than 20% of the monthly cost of service

Stakater shall not be considered to have violated the SLA and shall not be deemed liable if the service level cannot be guaranteed for reasons beyond Stakater's control.

If the SLA is violated for multiple availability types for the same cluster simultaneously, only the highest penalty for the availability type shall be subject to payment.

## Additional Sections

The following sections from the `SAAP` SLA also applies to the `Managed OpenShift Service` SLA:

* [Excused Downtime](../saap-sla/saap-sla.md#6-excused-downtime)
* [Monthly Uptime Percentage](../saap-sla/saap-sla.md#7-monthly-uptime-percentage)
* [Limitations](../saap-sla/saap-sla.md#10-limitations)
* [SLA Exclusions](../saap-sla/saap-sla.md#13-sla-exclusions)
