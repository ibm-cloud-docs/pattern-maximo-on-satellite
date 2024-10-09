---

copyright:
  years: 2024
lastupdated: "2024-05-07"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

---

{{site.data.keyword.attribute-definition-list}}

# Architecture decisions for data
{: #data-architecture}

There are 2 sets of architectural decisions in this pattern, one pertains to {{site.data.keyword.satellitelong_notm}} and the other to {{site.data.keyword.prodname_imas_full_notm}}.

## Architecture decisions for data in {{site.data.keyword.prodname_imas_short}}
{: #data-residency-mas}

The following are architecture decisions about data for {{site.data.keyword.prodname_imas_short}}.

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Data store | {{site.data.keyword.prodname_imas_short}} configuration data is stored securely | Store data in MongoDB | Configure MongoDB and at a minimum, the MongoDB administrator is required to have database table creation privileges. | MongoDB is a prerequisite for {{site.data.keyword.prodname_imas_short}}. The MongoDB instance must support the transport layer security (TLS) communication protocol. For more information, see [TLS/SSL (Transport Encryption)](https://www.mongodb.com/docs/manual/core/security-transport-encryption/){: external}.  |
{: caption="Architecture decisions for data related to {{site.data.keyword.prodname_imas_short}}" caption-side="bottom"}


## Architecture decisions for data in Satellite
{: #data-residency-sat}

The following are architecture decisions about data for {{site.data.keyword.satellitelong_notm}}.

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Data residency | Data should be stored within the country or geographical region | - Store data in {{site.data.keyword.satelliteshort}} location \n - Store data in {{site.data.keyword.Bluemix_notm}} | Store data in {{site.data.keyword.satelliteshort}} location | Deploy Cloud Object Storage in a {{site.data.keyword.satelliteshort}} location with sufficient computing hosts and raw block storage that is allocated for creating Cloud Object Storage. \n Enable {{site.data.keyword.Bluemix_notm}} Databases (ICD) for {{site.data.keyword.satelliteshort}} and deploy PostgreSQL or Redis ICD instances into a {{site.data.keyword.satelliteshort}} location. \n For more information, see [on-premises Cloud Object Storage](/docs/cloud-object-storage?topic=cloud-object-storage-about-cos-satellite) and [on-premises SAN storage](/docs/cloud-databases?topic=cloud-databases-satellite-on-prem). |
{: caption="Architecture decisions for data related to {{site.data.keyword.satellitelong_notm}}" caption-side="bottom"}
