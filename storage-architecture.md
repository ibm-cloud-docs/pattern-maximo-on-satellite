---

copyright:
  years: 2024
lastupdated: "2024-02-15"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

---

{{site.data.keyword.attribute-definition-list}}

# Architecture decisions for storage in MAS
{: #storage-decisions-mas}

The following sections summarize the storage architecture decisions for the pattern that involves deployment of Maximo® Application Suite (MAS) on an {{site.data.keyword.satellitelong_notm}} on-premises location.

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Data store | Data dictionary for MAS | - Enterprise Edition MongoDB \n - Community Edition MongoDB | Enterprise Edition MongoDB | Provides more security features and good for enterprise grade workloads |
| Database | Database for Maximo Manage | - Db2 \n - Db2 as part of Cloud Pak for Data (CP4D) | Db2 | Enterprise might already own Db2 license. [Db2 configuration](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=deployment-configuring-db2) is done before deploying MAS. |
{: caption="Table 1. Architecture decisions for storage in MAS" caption-side="bottom"}


# Architecture decisions for storage in Satellite
{: #storage-decisions-sat}

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Satellite hosts | Satellite hosts: Control plane | -  Host node local storage \n- Remote storage | Host node local storage | Virtual Machine disks: minimum 10 GB Boot disk (25 GB is recommended) plus 100 GB secondary disk (unformatted). For more details see [Satellite Host Storage Requirements](/docs/satellite?topic=satellite-reqs-host-storage) |
|  | Satellite Hosts: Worker Nodes | -  Host node local storage \n- Remote storage  | Host node local storage | Virtual Machine disks: minimum 10 GB Boot disk (25 GB is recommended) plus 100 GB secondary disk (unformatted). Additional disks/size depend on storage requirements for satellite-enabled services running in the Satellite Location. See AD for Satellite Enabled Services. See [Satellite Host Storage Requirements](/docs/satellite?topic=satellite-reqs-host-storage) |
| Storage | Satellite Services Storage: OpenShift (Customer Workloads) | -  File Storage \n- Block Storage \n- Object Storage \n- Software Defined Storage (SDS) | Software Defined Storage (SDS) | SDS for container environments provide highly available and scalable storage and support file, block, and cloud object storage types to meet the requirements of various containerized workloads. |
| | Software Defined Storage | -  OpenShift Data Foundation (ODF) \n- Portworx Enterprise | OpenShift Data Foundation (ODF) | SDS for container environments that supports file, block, and object storage types, high availability and data replication and encryption. Storage template available for integration/use with satellite-enabled services. |
| | | | Portworx Enterprise | SDS for container environments that supports file and block storage types, high availability and data replication and encryption. \n  Sample Portworx configuration: \n- Portworx key-value database (KVDB) for etcd (deploys DB on local disks). Requires additional disk in Satellite host nodes \n- Hyper-converged mode for best performance (compute and storage on same worker node) \n  Portworx Enterprise is available in the [IBM Cloud Catalog](/catalog/services/portworx-enterprise) and can be installed on any IBM-managed OpenShift Cluster (deployed on IBM Cloud or a Satellite location). See this [link](/docs/openshift?topic=openshift-portworx) for configuration details. |
|  | Portworx Enterprise Storage | -  Worker Node Host local disks \n- Remote storage | Worker Node Host local disks | One raw, unformatted disk for Portworx storage nodes.  Another disk for Portworx internal KVDB. |
|  | Satellite Services Storage Template: OpenShift | -  [Available Storage Templates List](/docs/satellite?topic=satellite-storage-template-ov#storage-template-ov-providers) \n- Other Storage (BYO Driver) | Storage Template | Satellite storage templates are provided and tested by IBM or third-party vendors, check the following link to get the supported providers. See [document](/docs/satellite?topic=satellite-storage-template-ov#storage-template-ov-providers) for details. |
|  | Satellite Services Storage Template: Other Satellite-Enabled Services | [Storage Templates](/docs/satellite?topic=satellite-storage-template-ov#storage-template-ov-providers) | Based on Satellite Enabled Service | Use Storage Template supported by the Satellite-Enabled Service; one Storage Template for each service. This reference solution doesn’t include any other Satellite-enabled services. |
|  | Storage: Backup | | | |
| | Satellite Control Plane | Cloud Object Storage (COS) | Cloud Object Storage (COS) | A customer-owned COS bucket must be provided to be used for IBM-managed backups of the Satellite location control plane data. See [Creating Satellite Locations](/docs/satellite?topic=satellite-locations) for details. |
{: caption="Table 2. Architecture decisions for storage in Satellite" caption-side="bottom"}
