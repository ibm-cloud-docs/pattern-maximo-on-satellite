---

copyright:
  years: 2025
lastupdated: "2025-06-17"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

---

{{site.data.keyword.attribute-definition-list}}

# Overview
{: #overview}



The objective of this document is to provide an IBM Solution Design for the deployment of {{site.data.keyword.prodname_imas_full_notm}} on {{site.data.keyword.satellitelong}} in an on-premises {{site.data.keyword.satelliteshort}} location. {{site.data.keyword.satellitelong_notm}} is a software platform that lets you provision-managed cloud services across any environment. {{site.data.keyword.prodname_imas_full_notm}} is a set of applications for asset monitoring, management, predictive maintenance, and reliability planning.
This document describes the configuration of an {{site.data.keyword.satellitelong_notm}} location, that would be on-premises, where {{site.data.keyword.prodname_imas_full_notm}} is deployed.

The pattern follows the {{site.data.keyword.IBM}} Architecture Design Framework and provides a solution design from the standard {{site.data.keyword.Bluemix_notm}} deployment architecture for these two facets of a {{site.data.keyword.satelliteshort}} solution:

- The managed from environment is {{site.data.keyword.Bluemix_notm}}.
- The managed to environment is the {{site.data.keyword.satelliteshort}} location.

•	Provide a prescriptive, end-2-end enterprise-class solution design, with diagrams, component architecture decisions for the satellite location.

•	Will highlight what {{site.data.keyword.prodname_imas_full_notm}} customers look for, namely secure fast responses. In keeping with that focus, the pattern addresses two key aspects of an {{site.data.keyword.satellitelong}} solution – network connectivity and security.

The objective of this pattern document is to serve as a guide to meet typical customer requirements and provide a base reference solution for a distributed cloud solution that is secure and resilient especially for customers moving from Maximo v7.x to {{site.data.keyword.prodname_imas_full_notm}} v9.x.

## Major components of the solution
{: #massat-components}

{{site.data.keyword.satelliteshort}} has two major components that is configured first:
- The {{site.data.keyword.satelliteshort}} location management plane components along with the services that are required and available on {{site.data.keyword.Bluemix_notm}}.
- The {{site.data.keyword.satelliteshort}}-enabled services available at a {{site.data.keyword.satelliteshort}} location.

The Maximo Application Suite includes applications, such as Maximo Manage, Maximo Monitor, Maximo Health, Maximo Predict, Maximo Visual Inspection, and Maximo Assist.

Maximo MRO Inventory Optimization is a SaaS offering and not included in {{site.data.keyword.prodname_imas_full_notm}}. For more information, see [{{site.data.keyword.prodname_imas_full_notm}} architecture](/docs/en/masv-and-l/maximo-manage/cd?topic=SSLPL8_cd/com.ibm.mam.doc/upgrade/c_mas_architecture.htm).
{: note}

Maximo® Application Suite includes an entitlement to use Cloud Pak for Data (CP4D) and a rela inted Red Hat OpenShift subscription that's extended to cover MAS. There is also the option not to have the Red Hat OpenShift subscription included, for those customers that already have an Red Hat OpenShift subscription.

In this case the {{site.data.keyword.satelliteshort}} location would be configured on-premises. After which {{site.data.keyword.prodname_imas_full_notm}} v9.x would be set up at that location. This might serve as an upgrade pattern for customers who are currently using Maximo EAM v7. The equivalent functionality available is {{site.data.keyword.prodname_imas_full_notm}} v8 Manage.
