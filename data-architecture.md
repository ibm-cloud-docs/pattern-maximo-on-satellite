---

copyright:
  years: 2024
lastupdated: "2024-02-15"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

---

{{site.data.keyword.attribute-definition-list}}

# Architecture decisions for data
{: #data-architecture}

The following tables summarize the data architecture decisions for the deployment of Maximo® Application Suite (MAS) on an {{site.data.keyword.satellitelong_notm}} on-premises location.

## Architecture decisions for data
{: #data-residency}

The following are architecture decisions for data for this design.

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Data residency | Data should stay in the region | - Store data in {{site.data.keyword.satelliteshort}} location \n - Store data in {{site.data.keyword.Bluemix_notm}} | Store data in {{site.data.keyword.satelliteshort}} location | Deploy Cloud Object Storage (COS) in a {{site.data.keyword.satelliteshort}} location with sufficient computing hosts and raw block storage allocated for provisioning Object Storage. \n  Enable {{site.data.keyword.Bluemix_notm}} Databases (ICD) for {{site.data.keyword.satelliteshort}} and deploy PostgreSQL or Redis ICD instances into a {{site.data.keyword.satelliteshort}} location. \n  See [on-premises Cloud Object Storage](/docs/cloud-object-storage?topic=cloud-object-storage-about-cos-satellite) and [on-premises SAN storage](/docs/cloud-databases?topic=cloud-databases-satellite-on-prem). |
{: caption="Table 1. Architecture decisions for data related to related to Maximo® Application Suite" caption-side="bottom"}



| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Data residency | Data should stay in the region | - Store data in {{site.data.keyword.satelliteshort}} location \n - Store data in {{site.data.keyword.Bluemix_notm}} | Store data in {{site.data.keyword.satelliteshort}} location | Deploy Cloud Object Storage (COS) in a {{site.data.keyword.satelliteshort}} location with sufficient computing hosts and raw block storage allocated for provisioning Object Storage. \n  Enable {{site.data.keyword.Bluemix_notm}} Databases (ICD) for {{site.data.keyword.satelliteshort}} and deploy PostgreSQL or Redis ICD instances into a {{site.data.keyword.satelliteshort}} location. \n  See [on-premises Cloud Object Storage](/docs/cloud-object-storage?topic=cloud-object-storage-about-cos-satellite) and [on-premises SAN storage](/docs/cloud-databases?topic=cloud-databases-satellite-on-prem). |
{: caption="Table 1. Architecture decisions for data related to {{site.data.keyword.satellitelong_notm}}" caption-side="bottom"}
