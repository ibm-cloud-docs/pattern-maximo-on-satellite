---

copyright:
  years: 2024
lastupdated: "2025-06-17"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

---

{{site.data.keyword.attribute-definition-list}}

# Storage design
{: #storage-design-mas}

{{site.data.keyword.prodname_imas_full_notm}} storage options are controlled at the system and application scope. For information about {{site.data.keyword.prodname_imas_full_notm}} scope definitions, see [Configuring Maximo Application Suite](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=configuring){: external}. {{site.data.keyword.prodname_imas_short}} application data and data analytics are stored in MongoDB which is a prerequisite for {{site.data.keyword.prodname_imas_full_notm}}. It is used as the data dictionary for {{site.data.keyword.prodname_imas_short}} Monitor application. It is also used as the default user registry. The MongoDB instance can run in the Red Hat OpenShift cluster or external to it.

Db2 Warehouse is not a prerequisite for Manage. Db2 11.5 can be used and is installed by the Db2 Universal Operator.
Db2 Warehouse is typically installed as part of {{site.data.keyword.Bluemix_notm}} Pak for Data. Create an IBM Db2 Warehouse database for exclusive use by {{site.data.keyword.prodname_imas_short}} Manage. You can't reuse a Db2 Warehouse database on {{site.data.keyword.Bluemix_notm}} Pak for Data that is already used by another deployed {{site.data.keyword.prodname_imas_full_notm}} application.
