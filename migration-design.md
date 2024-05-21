---

copyright:
  years: 2024
lastupdated: "2024-05-07"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

---

{{site.data.keyword.attribute-definition-list}}

# Migration design
{: #migration-design-mas}

The Maximo Application Suite (MAS) [migration process](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=overview-process){: external} consists of an initial test deployment followed by the production deployment after successful testing. A client with Maximo EAM 7.12+ can upgrade to Maximo Application Suite Manage and reuse its database. The upgrade process upgrades the data base. Since the upgrade also includes a rebase, if the client has integrations, those must be reimplemented in the new environment. Install Maximo Application Suite before deploying Maximo Manage as an application within it.

If possible, deploy Maximo Application Suite to one or more nonproduction environments that are hosted in {{site.data.keyword.satelliteshort}} locations on-premises. These can be used for testing before deploying the same to production. These might also be used as disaster recovery for Maximo application across {{site.data.keyword.satelliteshort}} locations.
{: note}

