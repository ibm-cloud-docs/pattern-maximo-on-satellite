---

copyright:
  years: 2024
lastupdated: "2024-02-15"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

---

{{site.data.keyword.attribute-definition-list}}

# Service Management design
{: #service-mgt-design}

From a monitoring perspective, use:
- Application level metrics and dashboards provided by IBM® Maximo® Application Suite (MAS) applications. They monitor various aspects to report about application health and performance.
- Red Hat® OpenShift® cluster's preconfigured Grafana instance to visualize Prometheus metrics from compute nodes in the cluster.
[Refer](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=monitoring)

From an audit logging perspective, MAS logs can be aggregated from a Red Hat® OpenShift® cluster to third-party systems. [Refer](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=administering-audit-logging-in-maximo-application-suite)

MAS container logs i.e. pods in the core namespace contain audit log entries. For container and application logs, IBM Log Analysis works out of the box with Red Hat OpenShift clusters hosted in IBM Cloud. Note, MAS audit logs are unavailable for forwarding for IBM Cloud® when the Red Hat® OpenShift® logging subsystem is used.
