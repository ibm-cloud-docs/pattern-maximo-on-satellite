---

copyright:
  years: 2024
lastupdated: "2024-05-13"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

---

{{site.data.keyword.attribute-definition-list}}

# Service Management design
{: #service-mgt-design}

From a monitoring perspective, use the following :
- Application level metrics and dashboards provided by IBM Maximo®Application Suite (MAS) applications. They monitor various aspects to report about application health and performance. It's recommended to use Prometheus as the tool for app monitoring?
- Red Hat OpenShift cluster's preconfigured Grafana instance to visualize Prometheus metrics from compute nodes in the cluster. For more information, see [Monitoring Maximo Application Suite](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=monitoring){: external}.
- Use {{site.data.keyword.Bluemix_notm}} Monitoring for ROKS cluster health monitoring

From an audit logging perspective, the [MAS logs](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=administering-audit-logging-in-maximo-application-suite){: external} can be aggregated from a Red Hat OpenShift cluster to third-party systems.

MAS container logs, for example, pods, in the core namespace contain audit log entries. For container and application logs, {{site.data.keyword.Bluemix_notm}} logs service works out of the box with Red Hat OpenShift clusters hosted in {{site.data.keyword.Bluemix_notm}}.

 MAS audit logs are unavailable for forwarding for {{site.data.keyword.Bluemix_notm}}® when the Red Hat® OpenShift® logging subsystem is used.
 {: note}
