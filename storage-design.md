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

Maximo® Application Suite (MAS) storage options are controlled at the system and application scope. MAS application data and data analytics are stored in MongoDB which is a prerequisite for MAS. It is used as the data dictionary for MAS and its applications. It is also used as the default user registry. The MongoDB instance can run in the Red Hat® OpenShift® cluster or external to it.

Db2 Warehouse is usually configured at the systen scope for Maximo Monitor application and the IoT tool while object storage is a configured for Maximo Assist. Db2 Warehouse is typically installed as part of IBM Cloud Pak for Data (CP4D), but it can also be installed standalone for Maximo Manage.

MAS scope definitions can be found [here](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=configuring.)
