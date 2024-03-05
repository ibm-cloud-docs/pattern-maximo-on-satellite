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

## Architecture decisions for high availability
{: #high-availability}

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| High availability deployment | Ensure availability of MAS nodes | - Single zone deployment \n Multi-zone deployment	| Multi-zone deployment	| Minimum of 3 hosts and place the host machines in physically different racks. Power, network, and storage isolation and even separate data centers recommended for protection against outages for any of these components. For more information, see [{{site.data.keyword.satelliteshort}} HA considerations](/docs/satellite?topic=satellite-ha). |
| High Availability | Red Hat OpenShift workloads | \n - Single zone Red Hat OpenShift cluster \n - Multi-zone Red Hat OpenShift cluster | Multi-zone Red Hat OpenShift cluster | Configure Red Hat OpenShift clusters with a minimum of 3 worker nodes and spares across 3 zones. Size the worker nodes in each zone at 50% of required CPU capacity for workloads to meet 100% capacity requirements because of a zone failure. |
{: caption="Table 1. High availability architecture decisions" caption-side="bottom"}

## Architecture decisions for backup and restore
{: #backup-and-restore}

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Backup |  {{site.data.keyword.satelliteshort}} control plane data | {{site.data.keyword.IBM_notm}} managed backups in {{site.data.keyword.cos_full_notm}} |{{site.data.keyword.IBM_notm}} managed backups in {{site.data.keyword.cos_full_notm}}| {{site.data.keyword.IBM_notm}} {{site.data.keyword.satelliteshort}} service backs up {{site.data.keyword.satelliteshort}} control plane data as follows. For more information, see [Securing your Data](/docs/satellite?topic=satellite-data-security) \n {{site.data.keyword.satelliteshort}} control plane master data backups in {{site.data.keyword.IBM_notm}} owned {{site.data.keyword.cos_full_notm}} instance every hour \n {{site.data.keyword.satelliteshort}} enabled services master data backups in customer-owned {{site.data.keyword.cos_full_notm}} instance every 8 hours |
| Backup | OpenShift clusters | - Portworx PX backup for Kubernetes \n Kasten by Veeam \n Triliovault for Kubernetes \n Bring your own backup tool | Portworx PX Backup for Kubernetes | Use the PX-Backup add-on to Portworx Enterprise to backup application data, configuration, and Kubernetes objects at the Kubernetes pod, namespace, or cluster level. \n Backups can be stored in a customer-owned {{site.data.keyword.cos_full_notm}} instance.|
{: caption="Table 2. Backup and restore architecture decisions" caption-side="bottom"}


## Architecture decisions for high availability
{: #high-availability}

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| High availability deployment| Ensure availability of {{site.data.keyword.satelliteshort}} host nodes: Control and worker nodes | - Single zone deployment \n Multi-zone deployment	| Multi-zone deployment	| Minimum of 3 hosts and spares across the 3 zones Place the host machines in physically different racks. Power, network, and storage isolation and separate data centers recommended for protection against outages for any of these components. Separate physical locations (<100 ms latency) are recommended for protection against data center outages. For more information, see [{{site.data.keyword.satelliteshort}} HA considerations](/docs/satellite?topic=satellite-ha). |
| High Availability | Red Hat OpenShift workloads | \n - Single zone Red Hat OpenShift cluster \n - Multi-zone Red Hat OpenShift cluster | Multi-zone Red Hat OpenShift cluster | Configure Red Hat OpenShift clusters with a minimum of 3 worker nodes and spares across 3 zones. Size the worker nodes in each zone at 50% of required CPU capacity for workloads to meet 100% capacity requirements because of a zone failure. |
{: caption="Table 1. High availability architecture decisions" caption-side="bottom"}

## Architecture decisions for backup and restore
{: #backup-and-restore}

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Backup |  {{site.data.keyword.satelliteshort}} control plane data | {{site.data.keyword.IBM_notm}} managed backups in {{site.data.keyword.cos_full_notm}} |{{site.data.keyword.IBM_notm}} managed backups in {{site.data.keyword.cos_full_notm}}| {{site.data.keyword.IBM_notm}} {{site.data.keyword.satelliteshort}} service backs up {{site.data.keyword.satelliteshort}} control plane data as follows. For more information, see [Securing your Data](/docs/satellite?topic=satellite-data-security) \n {{site.data.keyword.satelliteshort}} control plane master data backups in {{site.data.keyword.IBM_notm}} owned {{site.data.keyword.cos_full_notm}} instance every hour \n {{site.data.keyword.satelliteshort}} enabled services master data backups in customer-owned {{site.data.keyword.cos_full_notm}} instance every 8 hours |
| Backup | OpenShift clusters | - Portworx PX backup for Kubernetes \n Kasten by Veeam \n Triliovault for Kubernetes \n Bring your own backup tool | Portworx PX Backup for Kubernetes | Use the PX-Backup add-on to Portworx Enterprise to backup application data, configuration, and Kubernetes objects at the Kubernetes pod, namespace, or cluster level. \n Backups can be stored in a customer-owned {{site.data.keyword.cos_full_notm}} instance.|
{: caption="Table 2. Backup and restore architecture decisions" caption-side="bottom"}

---
| Architecture decision | Requirement | Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| High availability deployment | * Ensure availability of resources if outages occur. \n * Support SLA targets for availability. | - Single zone, single region \n - Multi zone, single region \n - Multi-zone, multi region | text | text|
| High availability infrastructure | * Ensure availability of infrastructure resources if outages occur. \n * Support SLA targets for infrastructure availability. | text | text | text|
| High availability application and database | * Ensure availability of application resources if outages occur. \n * Support SLA targets for application availability. | text | text | text|
{: caption="Table 1. High availability architecture decisions" caption-side="bottom"}

## Architecture decisions for backup and restore
{: #backup-and-restore}

| Architecture decision | Requirement | Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Infrastructure backup  | Backup images to enable recovery. | text | text | text |
| Database backup | Create transaction-consistent database backups to enable recovery of database tier if unplanned outages occur. |text | text | text |
| File backup | Create file system backups |text | text | text |
| Backup automation | Schedule regular database backups based on RPO requirements to enable data recovery if unplanned outages occur. |text | text | text |
{: caption="Table 2. Backup and restore architecture decisions" caption-side="bottom"}

## Architecture decisions for disaster recovery
{: #disaster recovery}

| Architecture decision | Requirement | Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Disaster recovery - application | Application disaster recovery capability in secondary region to meet RTO/RPO requirements| text | text | text |
| Disaster recovery - database                        | Database recovery capability in secondary region | text | Continuous replication of data from a primary to a secondary system in a separate region, including in-memory loading, system replication facilitates rapid failover in the event of a disaster|
| Disaster recovery - infrastructure | Infrastructure disaster recovery capability in secondary region to meet RTO/RPO requirements| text | text | text |
{: caption="Table 2. Disaster recovery architecture decisions" caption-side="bottom"}
