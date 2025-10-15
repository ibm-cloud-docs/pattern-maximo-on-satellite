---

copyright:
  years: 2024
lastupdated: "2025-06-17"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

---

{{site.data.keyword.attribute-definition-list}}

# Migration design
{: #migration-design-mas}

The {{site.data.keyword.prodname_imas_full_notm}} [migration process](https://www.ibm.com/docs/en/masv-and-l/cd?topic=overview-process){: external} consists of an initial test deployment followed by the production deployment after successful testing. A client with Maximo EAM 7.12+ can upgrade to {{site.data.keyword.prodname_imas_short}} Manage and reuse its database. The upgrade process upgrades the data base. Since the upgrade also includes a rebase, if the client has integrations, those must be reimplemented in the new environment. Install {{site.data.keyword.prodname_imas_short}} before deploying {{site.data.keyword.prodname_imas_short}} Manage as an application within it.

If possible, deploy {{site.data.keyword.prodname_imas_short}} to one or more nonproduction environments that are hosted in {{site.data.keyword.satelliteshort}} on-premises locations. These can be used for testing before deploying the same to production. These might also be used as disaster recovery for {{site.data.keyword.prodname_imas_short}} application across {{site.data.keyword.satelliteshort}} locations.
{: note}
