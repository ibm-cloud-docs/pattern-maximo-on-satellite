---

copyright:
  years: 2024
lastupdated: "2024-02-15"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

authors:
- name: Ashok Iyengar
- url: https://linkedin.com/in/ashokiyengar

# The release that the reference architecture describes
version: 1.0

# Use if the reference architecture has deployable code.
# Value is the URL to land the user in the IBM Cloud catalog details page for the deployable architecture.
# See https://test.cloud.ibm.com/docs/get-coding?topic=get-coding-deploy-button
deployment-url:

docs: https://cloud.ibm.com/docs/pattern-maximo-on-satellite

# use-case from 'code' column in
# https://github.ibm.com/digital/taxonomy/blob/main/topics/topics_flat_list.csv
use-case: Enterprise asset management

content-type: reference-architecture

---
<!--
The following line inserts all the attribute definitions. Don't delete.
-->
{{site.data.keyword.attribute-definition-list}}

# Deploy Maximo Application Suite in on-premises Satellite location
{: #maximo-on-satellite}
{: toc-content-type="reference-architecture"}
{: toc-use-case="Enterprise asset management"}
{: toc-version="1.0"}

IBM® Maximo® Application Suite (MAS) on {{site.data.keyword.satelliteshort}} pattern basically involves:
- An {{site.data.keyword.satellitelong_notm}} location configured on-premises
- Configuring MAS at that {{site.data.keyword.satelliteshort}} location

Due to privacy, regulatory, or compliance reasons, customers might not want to store their data in the public cloud. In such scenarios, the best option is to create one or more {{site.data.keyword.satelliteshort}} locations on-premises and host the MAS-related data locally.

## Architecture diagram
{: #architecture-diagram}

Figure 1 illustrates the {{site.data.keyword.satellitelong_notm}} architecture where the {{site.data.keyword.satelliteshort}} location is deployed on-premises and MAS installed at that location.

![MAS on-premises Satellite architecture](/images/MAS-on-premises-SatLoc-architecture.svg){: caption="Figure 1. Solution architecture showing MAS setup at an {{site.data.keyword.satellitelong_notm}} on-premises location" caption-side="bottom"}

Figure 2 shows the components in a MAS architecture. A detailed description of the MAS architecture can be found [here](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=models-maximo-application-suite-architecture).

![MAS architecture](/images/MAS-architecture.png){: caption="Figure 2. IBM Maximo Application Suite architecture" caption-side="bottom"}

## Design scope <!-- H2 -->
{: #design-scope}

The base {{site.data.keyword.satellitelong_notm}} solution covers design considerations and architecture decisions for the following aspects and domains:

- **Application Platform:** Enterprise Applications

- **Compute:** Bare Metal, Virtual Servers, Virtualization, Containers

- **Storage:** Primary Storage, Backup Storage

- **Networking:** Enterprise Connectivity, Network Segmentation

- **Data:** Databases & Data Storage (highlighting the Data Residency requirement)

- **Security:** Data Security, Identity and Access Management, Infrastructure and Endpoint

- **Resiliency:** Backup and Restore, High Availability

- **Service Management:** Monitoring, Logging, Auditing/Tracking

The [Introduction to the architecture framework](/docs/architecture-framework?topic=architecture-framework-intro), provides a consistent approach to design cloud solutions by addressing requirements across a pre-defined set of aspects and domains, which are technology-agnostic architectural areas to consider for any enterprise solution. It can be used as a guide to make the necessary design and component choices. After you have identified the applicable requirements and domains that are in scope, you can evaluate and select the best fit for purpose components for your enterprise cloud solution.

In Figure 2, you can view the domains that are relevant in a Maximo Application Suite on {{site.data.keyword.satellitelong_notm}} solution.

![MAS on {{site.data.keyword.satelliteshort}} architecture framework](/images/MAS-Satellite-AF.svg){: caption="Figure 3. MAS on {{site.data.keyword.satellitelong_notm}} Architecture Framework" caption-side="bottom"}

The Architecture Framework, described in [Introduction to the Architecture Framework](/docs/architecture-framework?topic=architecture-framework-intro), provides a consistent approach to design cloud solutions by addressing requirements across a pre-defined set of aspects and domains, which are technology-agnostic architectural areas that need to be considered for any enterprise solution. It can be used as a guide to make the necessary design and component choices to ensure you have considered applicable requirements for each aspect and domain. After you have identified the applicable requirements and domains that are in scope, you can evaluate and select the best fit for purpose components for your enterprise cloud solution.

Figure 3 shows the domains that are covered in this solution.


## Solution components and requirements for {{site.data.keyword.satelliteshort}} location on-premises
{: #solution-components-on-prem}

Review the following requirements and components for configuring MAS in an on-premises {{site.data.keyword.satelliteshort}} location.

## Requirements <!-- H2 -->
{: #requirements}

<!-- insert the requirements table, below is an example -->

The following table represents a baseline set of requirements, which are applicable to many clients who are looking to upgrade from Maximo 7.x to Maximo Application Suite (MAS) 8.x. Deployment of MAS on {{site.data.keyword.satellitelong_notm}} location serves as the first step.

| Aspect | Requirement |
|---|---|
| Application platform | Solution should to be fully managed from end to end |
| Compute | Customer is looking to deploy hosts running managed Red Hat® OpenShift Kubernetes Service (ROKS) clusters in the {{site.data.keyword.satelliteshort}} location |
| Storage | Provide storage that meets the MAS applications and database performance requirements |
| Network | Provide secure, low-latency connectivity |
| Data | - Data security and compliance requirements require that the data remain on-premises. \n -  Use a proven relational Database technology in order to provide critical information to applications on premises. |
| Security | Encrypt all application data in transit and at rest to protect it from unauthorized disclosure. |
| Resiliency | - Multi-site capability to support a disaster recovery strategy and solution that uses {{site.data.keyword.Bluemix_notm}} infrastructure DR capabilities that are combined with {{site.data.keyword.satelliteshort}} features. \n - Provide backups for MAS data retention. |
| Service management | Customer wants a fully managed service |
| Other | Shorten the time required to upgrade from Maximo 7.x to MAS 8.x |
| | Use a managed ROKS service helping customers that might not have the level of skill in OpenShift to operate it to the level required |
| | Provide an Image Replication migration solution that will minimize disruption during cut-over |
| | Access customer's existing Red Hat® Container Registry |
| | Use multiple {{site.data.keyword.satelliteshort}} locations to enable DR for MAS applications |
{: caption="Table 1. Pattern requirements" caption-side="bottom"}

{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.satelliteshort}} is a fully managed offering and there are certain responsibilities that are shared by IBM and the customer. For more information about the table and the corresponding task details, see [{{site.data.keyword.satelliteshort}} responsibilities](/docs/satellite?topic=satellite-responsibilities).

## Components <!-- H2 -->
{: #components}

For a list of {{site.data.keyword.satelliteshort}}-related components please [see](https://cloud.ibm.com/docs/pattern-base-ibm-cloud-satellite). The table below lists the components for setting up Maximo Application Suite Core, on Red Hat® OpenShift on-premises as a Managed Cloud Service (aka ROKS) via IBM Cloud Satellite. It represents the minimum resources needed to successfully install medium-sized Maximo Application Suite Core. Note, more resources might be needed to support specific workloads. [See](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=overview-prerequisite-software)


| Aspect| Component| How the component is used |
|---|---|---|
| Compute | Hosts | Virtual machine (VM) or {{site.data.keyword.baremetal_short_sing}} \n Host OS: RHEL 8.x |
| | {{site.data.keyword.satelliteshort}} worker nodes hosts: \n Red Hat® OpenShift (Customer Workload Cluster) | 8 vCPU and 32 GB RAM x 6 |
| | {{site.data.keyword.satelliteshort}} worker nodes hosts : \n Other {{site.data.keyword.satelliteshort}}-enabled services | Based on {{site.data.keyword.satelliteshort}}-enabled service which includes MongoDB as required by MAS core. \n  This solution pattern does not include any other MAS application. |
| | Containers | Managed Red Hat® OpenShift on {{site.data.keyword.satelliteshort}} |
| | Red Hat® OpenShift cluster | Recommend using even-numbered Red Hat® OpenShift Container Platform versions  |
| | Red Hat® OpenShift cluster services | These services are required by MAS Core and all its applications. \n  - Red Hat®Certificate Manager \n - IBM Suite License Service \n - Service Binding Operator \n - User Data Servies (UDS). Note: Starting with MAS 8.10.10, UDS is replaced with IBM Data Reporter Operator (DRO). {: note} |
| | Workload isolation | Single cluster for all workloads |
| | Container Images Registry | - {{site.data.keyword.registrylong_notm}} on {{site.data.keyword.Bluemix_notm}} (cp.icr.io) \n - Quay Registry (quay.io) \n - Red Hat® Registry (registry.redhat.io) |
| | Bastion host | Bastion host, external to the RHOS is useful when installing MAS core, Cloud Pak for Data (CP4D), and other prerequisites into Red Hat® OpenShift cluster. |
| Storage: Primary | Red Hat® OpenShift cluster | Control plane worker nodes host local storage \n  Data plane worker nodes offer Red Hat® OpenShift Data Foundation (ODF) internal storage for application data, registry, logging, metrics. \n  Recommend 15 GB - 25 GB of disk storage per CPU allocated to the compute nodes. \n  Note: MAS provides a license for IBM Fusion Storage (with limitations) that includes the IBM delivery of ODF.|
| Storage: Backup | Red Hat® OpenShift workload data | Customer can choose to use Cloud Object Storage on {{site.data.keyword.Bluemix_notm}} |
| Networking | Enterprise Connectivity | MAS uses networking setup by Red Hat® OpenShift® Container Platform (RHOCP) for its internal communications. [See](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=premises-networking-considerations) |
| | | Connectivity from the cluster to external endpoints (except in an air-gapped deployment) |
| | | Connectivity into the cluster for Web Browsers to access the MAS control plane and applications |
| | | Connectivity from the Web Browsers to external Internet endpoints via port 443 |
| | Load balancers | External LB to access protocol endpoints that are used to communicate with  RHOCP and with the applications |
| | Segmentation | MAS is configured to enable least-privilege access throughout the product with a default deny-all policy |
| | Red Hat® OpenShift cluster | Container network policies |
| | DNS | Client DNS at {{site.data.keyword.satelliteshort}} location |
| Data | Data services | Dependent on MAS application. For MAS core only MongoDB is required.
| | MongoDB | MAS uses MongoDB for its data dictionary and local user management. In this solution, {{site.data.keyword.satelliteshort}}-enabled MongoDB service is used. |
| | Cloud Pak for Data Services | While MAS includes an entitlement to use Cloud Pak for Data, it is not a pre-requisite for MAS core. \n  DB2 Warehouse is another CP4D component that is used by MAS applications like Maximo Manage and Maximo Health. \n  Note: DB2 Warehouse is not a prereq for Manage. DB2 11.5 can be used and is installed via the DB2 Universal Operator. |
| Security | Connectivity | - DNS should contain the domain names  \n - Firewall if present should allow TCP/IP connections from RHOCP nodes to port 443 of external sites |
| Security: Data | | |
| Data encryption at rest | {{site.data.keyword.satelliteshort}} control plane backup storage | Cloud Object Storage encrypted with provider keys |
| | {{site.data.keyword.satelliteshort}} worker nodes data | Worker nodes storage encryption: Customer |
| | Red Hat® OpenShift cluster persistent storage | Cluster volume encryption with Kubernetes Secret |
| Data encyption in transit | {{site.data.keyword.satelliteshort}} Link | Encryption that uses TLS |
| | Red Hat® OpenShift cluster workloads | App-level encryption that uses TLS |
| | Certificate Issuer | By default, MAS provides a Cluster Issuer that generates self-signed certificates. Customers have the option to provide their Certificate Issuer. /n  MAS uses IBM® Certificate Manager for automatic management and issuance of TLS certificates. |
| Security: Identity and Access Management (IAM) | LDAP server \n  SAML server | The LDAP server must support the secure LDAP (LDAPS) protocol. Non-TLS connections are not supported. \n  MAS core maintains a registry of users. You can specify which users have access to which MAS applications. |
| | {{site.data.keyword.satelliteshort}} services: \n Red Hat® OpenShift (Customer Workloads Cluster) | - {{site.data.keyword.Bluemix_notm}} IAM Roles \n - Kubernetes role-based access control (RBAC) Roles |
| IAM: Application | Runtime security (WAF and DDoS) | Bring your own Edge Security | |
| IAM: Infrastructure & endpoint | Core Network Protection | Subnets and firewall rules | |
| IAM: Threat detection and response | Threat detection | Customer SIEM tool, for example, Splunk | |
| Resiliency: High availability | {{site.data.keyword.satelliteshort}} Host Nodes (control and worker nodes) | Multi-zone deployment | |
| | Red Hat® OpenShift workloads | Multi-zone Red Hat® OpenShift cluster | |
| Resiliency: Backup | Red Hat® OpenShift clusters | Portworx PX Backup for Kubernetes | IBM Fusion is recommended for MAS backup |
| Service management: Monitoring | IBM® Maximo® Application Suite | Configure Red Hat® OpenShift® cluster monitoring and install Grafana to monitor MAS \n - MAS uses the Prometheus monitoring stack within OCP for application level metrics \n - IBM {{site.data.keyword.satelliteshort}} Monitoring Tool for infrastructure |
| | Red Hat® OpenShift clusters | {{site.data.keyword.monitoringlong_notm}} | |
| Service management: Logging | {{site.data.keyword.satelliteshort}} location and hosts | - IBM {{site.data.keyword.satelliteshort}} {{site.data.keyword.loganalysisshort}} tool \n - {{site.data.keyword.loganalysislong}} |
| | Red Hat® OpenShift clusters | {{site.data.keyword.loganalysislong_notm}} |
| Service management: Auditing | {{site.data.keyword.satelliteshort}}e location events | {{site.data.keyword.cloudaccesstraillong}} |
| | Red Hat® OpenShift clusters | {{site.data.keyword.cloudaccesstraillong}} |
| Service management: Email | SMTP server | External SMTP server required to configure MAS core, Maximo Manage, and other applications to send emails to users. |
{: caption="Table 2. Pattern components" caption-side="bottom"}

As mentioned earlier, the Architecture Framework is used to guide and determine the applicable aspects and domains for which architecture decisions need to be made. The following sections contain the considerations, and architecture decisions for the aspects and domains that are in play in this solution pattern.
