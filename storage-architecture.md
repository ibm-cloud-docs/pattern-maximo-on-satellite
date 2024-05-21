---

copyright:
  years: 2024
lastupdated: "2024-05-13"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

---

# Architecture decisions for storage
{: #storage}

There are 2 sets of architectural decisions in this pattern, one pertains to {{site.data.keyword.satellitelong_notm}} and the other to {{site.data.keyword.prodname_imas_full_notm}}.

## Architecture decisions for storage in {{site.data.keyword.prodname_imas_short}}
{: #storage-decisions-mas}

The following are architecture decisions about storage for {{site.data.keyword.prodname_imas_short}}.

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Data store | Data dictionary for {{site.data.keyword.prodname_imas_short}} | - Enterprise Edition MongoDB \n - Community Edition MongoDB | Enterprise Edition MongoDB | Provides more security features and is a good option for enterprise grade workloads. |
| Database | Database for Maximo Manage | - Db2 \n - Db2 as part of Cloud Pak for Data | Db2 | The enterprise might already own Db2 license. [Db2 configuration](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=deployment-configuring-db2){: external} is done prior to deploying {{site.data.keyword.prodname_imas_short}}. |
{: caption="Table 1. Architecture decisions for storage in {{site.data.keyword.prodname_imas_short}}" caption-side="bottom"}


## Architecture decisions for storage in Satellite
{: #storage-decisions-sat}

The following are architecture decisions about storage for {{site.data.keyword.satellitelong_notm}}.

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Satellite hosts | Satellite hosts: Control plane | -  Host node local storage \n- Remote storage | Host node local storage | Virtual Machine disks: A minimum of 10 GB Boot disk (25 GB is recommended) plus 100 GB secondary disk that's unformatted. For more information, see [Satellite Host Storage Requirements](/docs/satellite?topic=satellite-reqs-host-storage). |
|  | Satellite Hosts: Worker Nodes | -  Host node local storage \n- Remote storage  | Host node local storage | Virtual Machine disks: A minimum of 10 GB Boot disk although 25 GB is recommended plus 100 GB secondary disk that's unformatted. Additional disks and size depend on storage requirements for satellite-enabled services running in the Satellite Location. For more information, see list of [Satellite Enabled Services](/docs/satellite?topic=satellite-managed-services) and [Satellite Host Storage Requirements](/docs/satellite?topic=satellite-reqs-host-storage) |
| Storage | Satellite Services Storage: OpenShift for Customer Workloads | -  File Storage \n- Block Storage \n- Object Storage \n- Software Defined Storage | Software Defined Storage | Software Defined Storage for container environments provide highly available and scalable storage and support file, block, and cloud object storage types to meet the requirements of various containerized workloads. |
| | Software Defined Storage | -  OpenShift Data Foundation \n- Portworx Enterprise | OpenShift Data Foundation | Software Defined Storage for container environments that supports file, block, and object storage types, high availability and data replication and encryption. Storage template available for integration and use with satellite-enabled services. |
|  | Satellite Services Storage Template: OpenShift | -  [Available Storage Templates List](/docs/satellite?topic=satellite-storage-template-ov#storage-template-ov-providers) \n- Other Storage, for example, Bring Your Own Driver | Storage Template | Satellite storage templates are provided and tested by IBM or third-party vendors, for more information, see [Which storage templates are available?](/docs/satellite?topic=satellite-storage-template-ov#storage-template-ov-providers). \n This reference solution doesn’t include any other Satellite-enabled services. |
|  | Storage: Backup | | | |
| | Satellite Control Plane | Cloud Object Storage | Cloud Object Storage | A customer-owned Cloud Object Storage bucket must be provided to be used for IBM-managed backups of the Satellite location control plane data. For more information, see [Creating Satellite Locations](/docs/satellite?topic=satellite-locations) for details. |
{: caption="Table 2. Architecture decisions for storage in {{site.data.keyword.satellitelong_notm}}" caption-side="bottom"}
