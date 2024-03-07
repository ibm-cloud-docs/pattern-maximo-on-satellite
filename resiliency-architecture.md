---

copyright:
  years: 2024
lastupdated: "2024-02-15"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS
---

# Architecture decisions for resiliency
{: #resiliency-architecture}

The following sections summarize the compute architecture decisions for the pattern that involves deployment of Maximo® Application Suite (MAS) on an {{site.data.keyword.satellitelong_notm}} on-premises location.

## Architecture decisions for high availability in MAS
{: #high-availability-mas}

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| High availability deployment | - Ensure availability of resources (MAS nodes) if outage occurs \n - Support SLA targets for availability | - Single node deployment \n - Multi-node deployment	| Multi-node deployment	| Minimum of 3 hosts. Place host machines in physically different racks. Power, network, and storage isolation and even separate data centers recommended for protection against outages for any of these components. \n  There are application services and data services that need to be spread across nodes (or zones) with an adequate level of replication configured. In addition to Suite services, each data service in MAS has different replication features. Refer to [MAS resiliency](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=availability-resilient-architecture-components) |
| High Availability infrastructure | - Ensure availability of infrastructure resources (Red Hat OpenShift cluster) if outage occurs \n - Support SLA targets for infrastructure availability | - Single node Red Hat OpenShift \n - Multi-node Red Hat OpenShift cluster | Multi-node Red Hat OpenShift cluster | - Configure Red Hat OpenShift clusters with a minimum of 3 worker nodes and 3 spares. \n - Size the worker nodes in each zone at 50% of required CPU capacity for workloads to meet 100% capacity requirements in case of rack failure. \n - Use pod topology spread constraints. |
{: caption="Table 1. High availability architecture decisions for MAS" caption-side="bottom"}

## Architecture decisions for backup and restore in MAS
{: #backup-and-restore-mas}

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Backup |  Persistence store data needs to be backed up | - Use backup capabilities of each persistence store \n - {{site.data.keyword.IBM_notm}} managed backups in {{site.data.keyword.cos_full_notm}} | Use backup capabilities of each persistence store | To restore the MAS instance, you must deploy or activate another database instance, and then restore the data from a backup. Refer to [MAS backup & restore](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=administering-backing-up-restoring-maximo-application-suite) |
| Backup | Backup Red Hat OpenShift clusters | - Roll your own backup strategy \n - Use the underlying {{site.data.keyword.satelliteshort}} backup & restore capabilities | Use the underlying {{site.data.keyword.satelliteshort}} backup & restore capabilities | The {{site.data.keyword.satelliteshort}} platform will handle backup & restore tasks. \n  Look at restoring data to a different Red Hat® OpenShift® cluster if there is an outage |
{: caption="Table 2. Backup and restore architecture decisions for MAS" caption-side="bottom"}


## Architecture decisions for high availability in Satellite
{: #high-availability-sat}

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| High availability deployment| Ensure availability of {{site.data.keyword.satelliteshort}} host nodes: Control and worker nodes | - Single rack deployment \n Multi-rack deployment	| Multi-rack deployment	| Minimum of 3 hosts and spares across the 3 racks. Place the host machines in physically different racks. Power, network, and storage isolation and separate data centers recommended for protection against outages for any of these components. Separate physical locations (<100 ms latency) are recommended for protection against data center outages. For more information, see [{{site.data.keyword.satelliteshort}} HA considerations](/docs/satellite?topic=satellite-ha). |
| High Availability | Red Hat OpenShift workloads | \n - Single node Red Hat OpenShift \n - Multi-node Red Hat OpenShift cluster | Multi-node Red Hat OpenShift cluster | Configure Red Hat OpenShift clusters with a minimum of 3 worker nodes and spares across 3 racks. Size the worker nodes in each rack at 50% of required CPU capacity for workloads to meet 100% capacity requirements because of a rack failure. |
{: caption="Table 3. High availability architecture decisions for Satellite" caption-side="bottom"}

## Architecture decisions for backup and restore in Satellite
{: #backup-and-restore-sat}

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Backup |  {{site.data.keyword.satelliteshort}} control plane data | {{site.data.keyword.IBM_notm}} managed backups in {{site.data.keyword.cos_full_notm}} | {{site.data.keyword.IBM_notm}} managed backups in {{site.data.keyword.cos_full_notm}}| {{site.data.keyword.IBM_notm}} {{site.data.keyword.satelliteshort}} service backs up {{site.data.keyword.satelliteshort}} control plane data as follows. For more information, see [Securing your Data](/docs/satellite?topic=satellite-data-security) \n {{site.data.keyword.satelliteshort}} control plane master data backups in {{site.data.keyword.IBM_notm}} owned {{site.data.keyword.cos_full_notm}} instance every hour \n {{site.data.keyword.satelliteshort}} enabled services master data backups in customer-owned {{site.data.keyword.cos_full_notm}} instance every 8 hours |
| Backup | Red Hat OpenShift clusters | - Portworx PX backup for Kubernetes \n Kasten by Veeam \n Triliovault for Kubernetes \n Bring your own backup tool | Portworx PX Backup for Kubernetes | Use the PX-Backup add-on to Portworx Enterprise to backup application data, configuration, and Kubernetes objects at the Kubernetes pod, namespace, or cluster level. \n Backups can be stored in a customer-owned {{site.data.keyword.cos_full_notm}} instance.|
{: caption="Table 4. Backup and restore architecture decisions for Satellite" caption-side="bottom"}

<!--
| Architecture decision | Requirement | Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| High availability deployment | * Ensure availability of resources if outages occur. \n * Support SLA targets for availability. | - Single zone, single region \n - Multi zone, single region \n - Multi-zone, multi region | text | text|
| High availability infrastructure | * Ensure availability of infrastructure resources if outages occur. \n * Support SLA targets for infrastructure availability. | text | text | text|
| High availability application and database | * Ensure availability of application resources if outages occur. \n * Support SLA targets for application availability. | text | text | text|
{: caption="Table 1. High availability architecture decisions" caption-side="bottom"}


## Architecture decisions for disaster recovery for Satellite
{: #disaster recovery-sat}

| Architecture decision | Requirement | Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Disaster recovery - application | Application disaster recovery capability in secondary region to meet RTO/RPO requirements| text | text | text |
| Disaster recovery - database    | Database recovery capability in secondary region | text | Continuous replication of data from a primary to a secondary system in a separate region, including in-memory loading, system replication facilitates rapid failover in the event of a disaster|
| Disaster recovery - infrastructure | Infrastructure disaster recovery capability in secondary region to meet RTO/RPO requirements| text | text | text |
{: caption="Table 2. Disaster recovery architecture decisions" caption-side="bottom"}
-->
