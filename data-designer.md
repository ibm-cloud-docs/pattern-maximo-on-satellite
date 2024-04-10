---

copyright:
  years: 2024
lastupdated: "2024-02-15"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

---

{{site.data.keyword.attribute-definition-list}}

# Data design
{: #data-design}

IBM® Maximo® Application Suite (MAS) is all about data since it is primarily an Enterprise Asset Management software. As an application suite it now has a set of applications for asset monitoring, management, predictive maintenance, and reliability planning.

MongoDB is a prerequisite for MAS. It is used as the data dictionary for MAS and its applications. It is also used as the default user registry. The MongoDB instance can run in the Red Hat® OpenShift® cluster or external to it.

IBM® User Data Services was used to collect, transform, and transmit Maximo usage data. Starting in IBM Maximo Application Suite 8.11.7 and 8.10.10, the User Data Services (UDS) is replaced with IBM Data Reporter Operator (DRO).
DRO is a prerequisite software for Maximo. It has a reduced operational footprint and cost than IBM User Data Services.

Many enterprises want to keep their data on-premises. This maximo-on-satellite pattern helps enterprises do that by deploying MAS in an on-premises {{site.data.keyword.satelliteshort}} location.
