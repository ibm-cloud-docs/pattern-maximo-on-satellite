---

copyright:
  years: 2024
lastupdated: "2024-01-23"

subcollection: <repo-name>

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Overview
{: #overview}

<!-- Note to author>    THIS SHOULD BE ABOUT 10 – 15 LINES AND FOLLOW….
The objective of this pattern is to provide a solution design for……. -->

The objective of this document is to provide an IBM Solution Design for the deployment of Maximo on IBM Cloud Satellite in an on-premises Satellite location. IBM Cloud Satellite is a software platform that lets you provision managed cloud services across any environment. IBM Maximo® Application Suite (MAS) is a set of applications for asset monitoring, management, predictive maintenance, and reliability planning.
This document describes the configuration of an IBM Cloud Satellite location, that would be on-premises, where MAS would be deployed.

The pattern follows the {{site.data.keyword.IBM}} architecture framework and provides a solution design from the standard {{site.data.keyword.Bluemix_notm}} deployment architecture for these two facets of a {{site.data.keyword.satelliteshort}} solution:

- Managed from: The managed from environment is {{site.data.keyword.Bluemix_notm}}.
- Managed to: The managed to environment is the {{site.data.keyword.satelliteshort}} location.

•	Provide a prescriptive, end-2-end enterprise-class solution design, with diagrams, component architecture decisions for the satellite location mentioned above.

•	Will highlight what MAS customers look for, namely secure fast responses. In keeping with that focus, the pattern addresses two key aspects of an {{site.data.keyword.satellitelong}} solution – network connectivity and security.

The objective of this pattern document is to serve as a guide to meet typical customer requirements and provide a base reference solution for a distributed cloud solution that is secure and resilient especially for customers moving from Maximo 7.x to MAS 8.x.

## {{site.data.keyword.satelliteshort}} components
{: sat-components}

There are two major components in {{site.data.keyword.satelliteshort}}:
- The management plane components along with the services that are available on {{site.data.keyword.Bluemix_notm}}.
- The {{site.data.keyword.satelliteshort}}-enabled services available at a {{site.data.keyword.satelliteshort}} location.


The Architecture Framework provides a consistent approach to design cloud solutions by addressing requirements across a set of "aspects" and "domains", which are technology-agnostic architectural areas that need to be considered for any enterprise solution. For more details, see [Introduction to the Architecture Framework](/docs/architecture-framework).
