---

copyright:
  years: 2024
lastupdated: "2024-05-13"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

---

# Architecture decisions for resiliency
{: #resiliency}

## Resiliency design MAS
{: #resiliency-design-mas}

High availability is provided by the main components of IBM Maximo Application Suite (MAS). MAS core services are deployed automatically with any instance. These services handle the basic administration and configuration of the suite, and they store metadata in a deployed MongoDB in a three-node instance. See [MAS logical architecture](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=availability-logical-architecture){: external}.

MAS has the ability to configure services to automatically restart after a failure and keep multiple instances of the service in operation. MAS application services use their own persistence stores that have some flexibility for the instance location. In particular, the application state and user data are spread across the following types of persistence stores. You can restore individual IBM Maximo Application Suite applications from your backups. While there are different choices, the ones relevant to this pattern are shown in Table 1 along with how resiliency is handled by that component:

Maximo Application Suite provides resiliency through suite service instances, availability zones (AZs), and storage. For more information, see [Resilient architecture components](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=availability-resilient-architecture-components){: external}.
- Recommendation is to [back up](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=suite-maximo-application-core){: external} MAS core databases and the namespace in Red Hat® OpenShift®.
- Suite services: Services are configured to automatically restart after a failure and keep multiple instances of the service in operation.
- Availability zones: In an on-premises setup there are no availability zones. Red Hat OpenShift worker nodes are configured across physical machines in the {{site.data.keyword.satelliteshort}} location and Kubernetes automatically schedules redundancy for the different pods.
- Storage: There is application code and configuration data. \n -- Application code: Product images can use pods to create multiple redundant copies. \n -- Configuration data: Kubernetes configuration secrets and configuration maps are held in etcd. Other configuration data is in MongoDB. Both use mirroring.

For more information, see [MAS resiliency pre-requisites](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=availability-resilient-architecture-components#concept_lpr_mxk_nwb__title__5){: external}. The following table shows the resiliency aspect for the four persistence stores.

 Persistence store | Recommended product | Resiliency |
|---|---|---|
| Document database | MongoDB | Resiliency is achieved by MongoDB technology, specifically using multiple nodes that handle connections and replicate data between the nodes. MAS uses a *write-to-primary-only* approach with a single data shared to simplify processing because this database has a relatively light transaction load. |
| Relational database | IBM® Db2® database | Relational database management system (RDBMS) resilience features are used. Whether workloads share a single relational database management system instance or are spread across multiple relational database management system instances, a backup scheduling strategy is required. |
| Cloud Object Storage | {{site.data.keyword.Bluemix_notm}}® Object Storage | A persistence store like Cloud Object Storage, has its own resilinece processes that are different from a relational database management system. You must consider the importance of data content versus storage space expense. |
| Red Hat OpenShift persistence storage | etcd | You can use built-in redundancy for greater hardware protection. |
{: caption="Table 1. Persistence storage products in MAS and their resilience features" caption-side="bottom"}

Lastly, the persistent volume claim data can be copied from the pod to Cloud Object Storage directly by creating a [network policy](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=pv-backing-up-persistent-volume-claim-data-cloud-object-storage). The network policy is needed because the MAS namespace blocks the egress network by default.


## Resiliency design for Satellite
{: #resiliency-design-sat}

From an {{site.data.keyword.satellitelong_notm}} perspective, high availability can be achieved on 3 levels: {{site.data.keyword.satellitelong_notm}} Management plane, {{site.data.keyword.satellitelong_notm}} Control plane, {{site.data.keyword.Bluemix_notm}} services. For more information, see [{{site.data.keyword.satelliteshort}} HA](https://cloud.ibm.com/docs/satellite?topic=satellite-ha).


| Component level | Description | Comments |
|---|---|---|
| {{site.data.keyword.satelliteshort}} management plane nodes | Choose an {{site.data.keyword.Bluemix_notm}} multizone metro that runs and manages the {{site.data.keyword.satelliteshort}} control plane of your location. IBM provides high availability | By default, the {{site.data.keyword.satelliteshort}} management plane is automatically set up with multiple instances and spread across multiple zones within the same {{site.data.keyword.Bluemix_notm}} multizone metro.|
| {{site.data.keyword.satelliteshort}} control plane nodes | Ensure the compute hosts in the {{site.data.keyword.satelliteshort}} location are set up highly available. High availability setup ensures that the {{site.data.keyword.satelliteshort}} control plane continues to run, even if compute hosts experience a power, networking, or storage outage. | Deploy compute hosts in multiples of 3. For this solution, 6 nodes are used. n\  Every compute host is on a separate physical host. |
| {{site.data.keyword.Bluemix_notm}} services | Every {{site.data.keyword.Bluemix_notm}} service running in the Satellite location, like Red Hat OpenShift on {{site.data.keyword.Bluemix_notm}}, comes with a set of options for how to increase service availability | Review the documentation of each service to find supported options. |
{: caption="Table 2. High availability in {{site.data.keyword.satelliteshort}} at three levels" caption-side="bottom"}
