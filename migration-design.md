---

copyright:
  years: 2024
lastupdated: "2024-02-15"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

---

{{site.data.keyword.attribute-definition-list}}

# Migration design
{: #migration-design-mas}

Maximo® Application Suite (MAS) [migration process](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=overview-process) consists of an initial test deployment followed by the production deployment after successful testing. The migration process does not support upgrading directly from Maximo Asset Management to Maximo Manage. You must install MAS first before you deploy Maximo Manage as an application within it.

Recommendation: If possible, deploy MAS to one or more non-production environments hosted in {{site.data.keyword.satelliteshort}}  locations on-premises. These can be used for testing before deploying the same to production.
