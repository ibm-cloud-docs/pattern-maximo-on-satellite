---

copyright:
  years: 2024
lastupdated: "2024-05-13"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

---

{{site.data.keyword.attribute-definition-list}}

# Security design
{: #security-design}

There are different facets to security in {{site.data.keyword.prodname_imas_full_notm}}.

- Credentials are kept in Red Hat OpenShift secrets.
- Access to the Red Hat OpenShift cluster nodes is only through the bastion host using private SSH key.
- Product images are pulled from authenticated IBM entitled registries.
- Users in {{site.data.keyword.prodname_imas_full_notm}} are created and managed at the suite level and are made available for application-level access with application-specific role assignments, like administrator or user.
- Application programming interface (API) keys can be generated and managed to be used in automation processes for user management in {{site.data.keyword.prodname_imas_full_notm}}.
- API Key generated in {{site.data.keyword.prodname_imas_full_notm}} Manage has a much broader scope than those generated to user management in {{site.data.keyword.prodname_imas_full_notm}} Core. For more information, see [Maximo Manage](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=manage-overview).

Security features from {{site.data.keyword.satellitelong_notm}} platform also come into play when setting up {{site.data.keyword.prodname_imas_full_notm}} on-premises in a {{site.data.keyword.satelliteshort}} location.
