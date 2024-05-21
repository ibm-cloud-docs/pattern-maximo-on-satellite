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

There are 2 main components in this pattern - {{site.data.keyword.prodname_imas_full_notm}} and {{site.data.keyword.satellitelong_notm}}. Servicing of {{site.data.keyword.prodname_imas_full_notm}} is described here.

From a monitoring perspective, use the following :
- Application level metrics and dashboards provided by {{site.data.keyword.prodname_imas_full_notm}} applications. They monitor various aspects to report about application health and performance. Administrators can configure Prometheus monitoring service and then use Grafana visualization software to view usage information.
- Red Hat OpenShift cluster's preconfigured Grafana instance to visualize Prometheus metrics from compute nodes in the cluster. For more information, see [Monitoring Maximo Application Suite](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=monitoring){: external}.
- Use {{site.data.keyword.Bluemix_notm}} Monitoring for ROKS cluster health monitoring

From an audit logging perspective, the [{{site.data.keyword.prodname_imas_short}} logs](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=administering-audit-logging-in-maximo-application-suite){: external} can be aggregated from a Red Hat OpenShift cluster to third-party systems.

{{site.data.keyword.prodname_imas_full_notm}} container logs, for example, pods, in the core namespace contain audit log entries. For container and application logs, {{site.data.keyword.Bluemix_notm}} logs service works out of the box with Red Hat OpenShift clusters hosted in {{site.data.keyword.Bluemix_notm}}.

 {{site.data.keyword.prodname_imas_full_notm}} audit logs are unavailable for forwarding for {{site.data.keyword.Bluemix_notm}}® when the Red Hat® OpenShift® logging subsystem is used.
 {: note}
