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

There are different facets to security in IBM® Maximo® Application Suite (MAS).

- Credentials are kept in Red Hat OpenShift secrets.
- Access to the Red Hat OpenShift cluster nodes is only through the bastion host using private SSH key.
- Product images are pulled from authenticated IBM entitled registries.
- MAS users are created and managed at the suite level and are made available for application-level access with application-specific role assignments, like administrator or user.
- Application programming interface (API) keys can be generated and managed to be used in automation processes for user management in MAS
- API Key generated in Manage has a much broader scope than those generated to user management in MAS Core.

Security features from {{site.data.keyword.satellitelong_notm}} platform also come into play when setting up MAS on-premises in a {{site.data.keyword.satelliteshort}} location.
