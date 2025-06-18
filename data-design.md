---

copyright:
  years: 2024
lastupdated: "2025-06-17"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

---

{{site.data.keyword.attribute-definition-list}}

# Data design
{: #data-design}

{{site.data.keyword.prodname_imas_full_notm}} is all about data since it's primarily an Enterprise Asset Management (EAM) software. As an application suite, it now has a set of applications for asset monitoring, management, predictive maintenance, and reliability planning.

MongoDB is a prerequisite for {{site.data.keyword.prodname_imas_short}}. It is used as the data dictionary for {{site.data.keyword.prodname_imas_short}} and its applications. It's also used as the default user registry. The MongoDB instance can run in the Red Hat OpenShift® cluster or externally to it.

IBM User Data Services was used to collect, transform, and transmit Maximo usage data. Starting in {{site.data.keyword.prodname_imas_full_notm}} 8.11.7 and 8.10.10, the User Data Services (UDS) is replaced with IBM Data Reporter Operator (DRO). Data Reporter Operator is a prerequisite software for {{site.data.keyword.prodname_imas_short}}. It has a reduced the operational footprint and cost than IBM User Data Services.

Many enterprises want to keep their data on-premises. This maximo-on-satellite pattern helps enterprises do that by deploying {{site.data.keyword.prodname_imas_short}} in an on-premises {{site.data.keyword.satelliteshort}} location.
