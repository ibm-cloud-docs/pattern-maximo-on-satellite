---

copyright:
  years: 2024
lastupdated: "2024-02-15"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

---

{{site.data.keyword.attribute-definition-list}}

# Storage design
{: #storage-design-mas}

Maximo® Application Suite (MAS) storage options are controlled at the system and application scope. MAS scope definitions can be found [here](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=configuring.) MAS application data and data analytics are stored in MongoDB which is a prerequisite for MAS. It is used as the data dictionary for Monitor application. It is also used as the default user registry. The MongoDB instance can run in the Red Hat® OpenShift® cluster or external to it.

Db2 Warehouse is not a prerequisite for Manage. Db2 11.5 can be used and is installed via the Db2 Universal Operator.
Db2 Warehouse is typically installed as part of IBM Cloud Pak for Data (CP4D). Create a IBM® Db2® Warehouse database for exclusive use by Maximo® Manage. You cannot reuse a Db2 Warehouse database on CP4D that is already used by another deployed MAS application.
