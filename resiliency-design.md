---

copyright:
  years: 2024
lastupdated: "2024-02-15"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

---

{{site.data.keyword.attribute-definition-list}}

# Resiliency design MAS
{: #resiliency-design-mas}

High availability is provided by the main components of MAS. The Maximo Application Suite core services are deployed automatically with any instance. These services handle the basic administration and configuration of the suite, and they store metadata in a deployed MongoDB in a three-node instance. See [MAS logical architecture](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=availability-logical-architecture)

Each of these application services uses their own persistence stores that have some flexibility for the instance location. In particular, the application state and user data are spread across the following types of persistence stores. While there are different choices, the ones relevant to this pattern is shown in the table 1 along with how resiliency is handled by that component:

Maximo® Application Suite provides resiliency through suite service instances, availability zones (AZs), and storage. See [Resilient architecture components](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=availability-resilient-architecture-components).
- Suite services: Services are configured to automatically restart after a failure and keep multiple instances of the service in operation.
- Availability zones: In an on-premises setup there are no AZs. Red Hat OpenShift worker nodes are configured across physical machines in the {{site.data.keyword.satelliteshort}} location and Kubernetes automatically schedules redundancy for the different pods.
- Storage: There is application code and configuration data. \n -- Application code - Product images can use pods to create multiple redundant copies. \n -- Configuration data - Kubernetes configuration secrets and configuration maps are held in etcd. Other configuration data is in MongoDB. Both use mirroring.

Refer to the [MAS resiliency pre-requisites](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=availability-resilient-architecture-components#concept_lpr_mxk_nwb__title__5). Table 1 shows the resiliency aspect for the four persistence stores.

 Persistence Store | Recommended Product | Resiliency |
|---|---|---|
| Document database | MongoDB | Resiliency is achieved by MongoDB technology, specifically using multiple nodes that handle connections and replicate data between the nodes. MAS uses a *write-to-primary-only* approach with a single data shard to simplify processing because this database has a relatively light transaction load. |
| Relational database | IBM® Db2® database | Relational database management system (RDBMS) resilience features are used. Whether workloads share a single RDBMS instance or are spread across multiple RDBMS instances, a backup scheduling strategy is required. |
| Cloud object storage (COS) | IBM Cloud® Object Storage | A persistence store like COS, has its own resilinece processes that are different from a RDBMS. One must consider the importance of data content versus storage space expense. |
| Red Hat® OpenShift® persistence storage | etcd | One can use built-in redundancy for greater hardware protection. |
{: caption="Table 1. Persistence storage products in use with MAS" caption-side="bottom"}

# Resiliency design Satellite
{: #resiliency-design-sat}

From an {{site.data.keyword.satellitelong_notm}} perspective, high availability can be achieved on 3 levels - {{site.data.keyword.satellitelong_notm}} Management plane, {{site.data.keyword.satellitelong_notm}} Control plane, IBM Cloud services. See [{{site.data.keyword.satelliteshort}} Link](docs/satellite?topic=satellite-ha).


| Component Level | Description | Comments |
|---|---|---|
| {{site.data.keyword.satelliteshort}} Management plane nodes | Choose an IBM Cloud multizone metro that runs and manages the {{site.data.keyword.satelliteshort}} control plane of your location. IBM provides high availability | By default, the {{site.data.keyword.satelliteshort}} management plane is automatically set up with multiple instances and spread across multiple zones within the same IBM Cloud multizone metro.|
| {{site.data.keyword.satelliteshort}} Control plane nodes | Ensure the compute hosts in the {{site.data.keyword.satelliteshort}} location are set up highly available. HA setup ensures that the {{site.data.keyword.satelliteshort}} control plane continues to run, even if compute hosts experience a power, networking, or storage outage | Deploy compute hosts in multiples of 3. For this solution 6 nodes are used. n\  Every compute host is on a separate physical host. |
| IBM Cloud Services | Every IBM Cloud service running in the Satellite location, like Red Hat OpenShift on IBM Cloud, comes with a set of options for how to increase service availability | Review documentation of each service to find supported options |
{: caption="Table 2. High availability in {{site.data.keyword.satelliteshort}} at three levels" caption-side="bottom"}
