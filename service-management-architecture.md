---

copyright:
  years: 2024
lastupdated: "2024-02-15"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

---

# Architecture decisions for service management
{: #service}

The following sections summarize the compute architecture decisions for the pattern that involves deployment of Maximo® Application Suite (MAS) on an {{site.data.keyword.satellitelong_notm}} on-premises location.

## Architecture decisions for monitoring in MAS
{: #monitoring-mas}

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Monitoring | Monitor MAS | Red Hat® OpenShift® cluster monitoring + Grafana | OpenShift® cluster monitoring + Grafana | MAS applications provide application level metrics and dashboards for monitoring application health and performance. \n RHOCP is preconfigured with a Grafana instance for visualizing Prometheus metrics from compute nodes in the cluster. |
| Operational monitoring of cloud infrastructure and services | Monitor system health to detect issues that might impact the availability of the system and application. | - IBM Cloud Monitoring \n - BYO Monitoring Tool | IBM Cloud Monitoring | IBM Cloud Monitoring collects and monitors operational metrics for cloud infrastructure as well as the cloud platform and services and provides a single view for all metrics |
{: caption="Table 1. Architecture decisions for monitoring in MAS" caption-side="bottom"}


## Architecture decisions for logging and audit logging in MAS
{: #auditing-mas}

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Audit logging | Aggregate and securely store audit logs | - Forward logs from Red Hat® OpenShift® to an external system \n - Use Red Hat® OpenShift® logging subsystem | Forward logs to [external system](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=administering-audit-logging-in-maximo-application-suite) | Most enterprises have external logging system |
| Log monitoring of DB | Monitor database logs to detect issues that might impact deployment/availability of databases | Database logs | DB logs | Use the DB logs along with IBM Cloud Logging to get more DB-specific log information. |
{: caption="Table 2. Architecture decisions for logging & audit logging in MAS" caption-side="bottom"}

## Architecture decisions for alerting in MAS
{: #alerting}

| Architecture decision | Requirement |  Option | Decision | Rationale |
|---|---|---|---|---|
| Operational alerts | Provide a mechanism to identify and send notifications about operational issues that are found across application and infrastructure. | - MAS built-in functionality  \n - IBM Cloud Monitoring +  IBM Cloud Logging + Event Notifications | MAS built-in functionality. | MAS has the ability to configure services to automatically restart after a failure and keep multiple instances of the service in operation. There's no need to define an alert and wait for it to notify operations personnel. |
{: caption="Table 3. Architecture decisions for alerting in MAS" caption-side="bottom"}




## Architecture decisions for monitoring in Satellite
{: #monitoring-sat}

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
|  Monitoring | Monitoring of {{site.data.keyword.satelliteshort}} location and hosts | - {{site.data.keyword.satellitelong_notm}} monitoring tool \n - {{site.data.keyword.monitoringlong}} |	{{site.data.keyword.satellitelong_notm}} monitoring tool | By default, {{site.data.keyword.satellitelong_notm}} automatically monitors and resolves certain alerts for the {{site.data.keyword.satelliteshort}} location setup and host infrastructure that can be accessed through {{site.data.keyword.satellitelong_notm}} console and CLI. \n For more information, see [Default monitoring for {{site.data.keyword.satelliteshort}}](docs/satellite?topic=satellite-monitor).|
| | | | {{site.data.keyword.monitoringlong}} | {{site.data.keyword.satellitelong_notm}} can be integrated with a customer-owned {{site.data.keyword.monitoringlong}} instance that is enabled for platform-level metrics to provide more detailed metrics. The monitoring instance can be configured to collect metrics for both the {{site.data.keyword.satelliteshort}} location and {{site.data.keyword.satelliteshort}}-enabled services that run in the {{site.data.keyword.satelliteshort}} location. |
|  | Monitoring Red Hat OpenShift clusters | - Prometheus and Grafana on Red Hat OpenShift \n - {{site.data.keyword.monitoringlong}} \n  - Customer monitoring tool | {{site.data.keyword.monitoringlong}} | Manually deploy monitoring agents in Red Hat OpenShift clusters to forward metrics to a customer-owned {{site.data.keyword.monitoringlong}} instance and get unified views of metrics for Red Hat OpenShift clusters and other cloud services that run at the {{site.data.keyword.satelliteshort}} location and within the {{site.data.keyword.satelliteshort}} managed-from region. For more information, see [Setting up monitoring for clusters](/docs/satellite?topic=satellite-monitor). |
{: caption="Table 4. Architecture decisions for monitoring in Satellite" caption-side="bottom"}

## Architecture decisions for logging in Satellite
{: #logging-sat}

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Logging  | Logging events from {{site.data.keyword.satelliteshort}} location and hosts | - {{site.data.keyword.satellitelong_notm}} {{site.data.keyword.loganalysisshort}} tool \n - {{site.data.keyword.loganalysislong_notm}} | {{site.data.keyword.satellitelong_notm}} log analysis tool | By default, {{site.data.keyword.satellitelong_notm}} automatically generates a set of logs for the {{site.data.keyword.satelliteshort}} location that can be accessed through the {{site.data.keyword.satellitelong_notm}} built-in log analysis dashboard tools. \n For more information, see [Analyzing Logs for {{site.data.keyword.satelliteshort}} Location](/docs/satellite?topic=satellite-health). The log analysis instance can be configured to collect metrics for both the {{site.data.keyword.satelliteshort}} location and {{site.data.keyword.satelliteshort}}-enabled services that run in the {{site.data.keyword.satelliteshort}} location. |
| | | | {{site.data.keyword.loganalysislong_notm}} | {{site.data.keyword.satellitelong_notm}} can be integrated with a customer provisioned {{site.data.keyword.loganalysislong_notm}} instance that is enabled for platform-level logs to get a comprehensive view and tools to manage logs for {{site.data.keyword.satellitelong_notm}} and other {{site.data.keyword.Bluemix_notm}} resources. |
|  | Logging events from Red Hat OpenShift clusters | - EFK stack on Red Hat OpenShift \n - {{site.data.keyword.loganalysislong_notm}} \n - Customer logging tool | {{site.data.keyword.loganalysislong_notm}} | Manually deploy logging agents in Red Hat OpenShift clusters to forward cluster logs to a customer-owned {{site.data.keyword.satellitelong_notm}} and get a comprehensive view of logs for Red Hat OpenShift clusters and other cloud services that run at the {{site.data.keyword.satelliteshort}} location and within the {{site.data.keyword.satelliteshort}} managed-from region. For more information, see [Setting up Logging for Clusters](/docs/satellite?topic=satellite-health). |
{: caption="Table 5. Architecture decisions for logging in Satellite" caption-side="bottom"}

## Architecture decisions for auditing in Satellite
{: #auditing-sat}

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Auditing | Tracking and auditing {{site.data.keyword.satelliteshort}} location events | {{site.data.keyword.cloudaccesstraillong}} | {{site.data.keyword.cloudaccesstraillong_notm}} | Customer-owned {{site.data.keyword.cloudaccesstraillong_notm}} instance for {{site.data.keyword.satellitelong_notm}} to forward audit events. {{site.data.keyword.cloudaccesstraillong_notm}} tracks how users and applications interact with {{site.data.keyword.satellitelong_notm}}. It can be used to investigate abnormal activity and critical actions and to comply with regulatory audit requirements. For more information, see [Auditing events for {{site.data.keyword.satelliteshort}}](/docs/satellite?topic=satellite-at_events). |
|  | Tracking and auditing Red Hat OpenShift clusters | - {{site.data.keyword.cloudaccesstraillong_notm}} \n - Customer tool | {{site.data.keyword.cloudaccesstraillong_notm}} | Red Hat OpenShift on {{site.data.keyword.Bluemix_notm}} automatically generates cluster management events and forwards these event logs to a customer-owned {{site.data.keyword.cloudaccesstraillong_notm}} instance. For more information, see [Events for {{site.data.keyword.satelliteshort}} clusters](/docs/satellite?topic=satellite-at_events). |
{: caption="Table 6. Architecture decisions for auditing in Satellite" caption-side="bottom"}
