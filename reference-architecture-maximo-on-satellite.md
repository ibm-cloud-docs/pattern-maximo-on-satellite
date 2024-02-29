---

copyright:
  years: 2024
lastupdated: "2024-02-15"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

authors:
- name: Ashok Iyengar

# The release that the reference architecture describes
version: 1.0

# Use if the reference architecture has deployable code.
# Value is the URL to land the user in the IBM Cloud catalog details page for the deployable architecture.
# See https://test.cloud.ibm.com/docs/get-coding?topic=get-coding-deploy-button
deployment-url:

docs: https://cloud.ibm.com/docs/pattern-maximo-on-satellite

content-type: reference-architecture

---
<!--
The following line inserts all the attribute definitions. Don't delete.
-->
{{site.data.keyword.attribute-definition-list}}

# Deploy Satellite on-premises or in hyperscaler
{: #maximo-on-satellite}
{: toc-content-type="reference-architecture"}
{: toc-use-case="Managed cloud"}
{: toc-version="1.0"}

The Maximo Application Suite (MAS) on {{site.data.keyword.satelliteshort}} pattern basically involves:
- One {{site.data.keyword.satellitelong_notm}} location configured on-premises
- Configuring MAS at that {{site.data.keyword.satelliteshort}} location

Due to privacy, regulatory, or compliance reasons, customers might not want to store their data in the public cloud. In such scenarios, the best option is to create one or more {{site.data.keyword.satelliteshort}} locations on-premises and host the MAS-related data locally.

## Architecture diagrams
{: #architecture-diagram}

Figure 1 illustrates the {{site.data.keyword.satellitelong_notm}} architecture where the {{site.data.keyword.satelliteshort}} location is deployed on-premises and MAS installed at that location.


![Satellite location on-premises architecture](/images/SatLoc-on-premises-architecture.svg){: caption="Figure 1. Solution architecture showing MAS setup at an {{site.data.keyword.satellitelong_notm}} on-premises location" caption-side="bottom"}




## Design scope <!-- H2 -->
{: #design-scope}

The base {{site.data.keyword.satellitelong_notm}} solution covers design considerations and architecture decisions for the following aspects and domains:

- **Compute:** Bare Metal, Virtual Servers, Virtualization, Containers

- **Storage:** Primary Storage, Backup Storage

- **Networking:** Enterprise Connectivity, Network Segmentation

- **Data:** Data Storage (highlighting the Data Residency requirement)

- **Security:** Data Security, Identity and Access Management, Infrastructure and Endpoint

- **Resiliency:** Backup and Restore, High Availability

- **Service Management:** Monitoring, Logging, Auditing/Tracking

The [Introduction to the architecture framework](/docs/architecture-framework?topic=architecture-framework-intro), provides a consistent approach to design cloud solutions by addressing requirements across a pre-defined set of aspects and domains, which are technology-agnostic architectural areas to consider for any enterprise solution. It can be used as a guide to make the necessary design and component choices. After you have identified the applicable requirements and domains that are in scope, you can evaluate and select the best fit for purpose components for your enterprise cloud solution.

In Figure 3, you can view the domains that are relevant in an {{site.data.keyword.satellitelong_notm}} solution.

![Base {{site.data.keyword.satelliteshort}} architecture framework](/images/Base-Satellite-AF.svg){: caption="Figure 3. Base {{site.data.keyword.satellitelong_notm}} Architecture Framework" caption-side="bottom"}

The Architecture Framework, described in [Introduction to the Architecture Framework](/docs/architecture-framework?topic=architecture-framework-intro), provides a consistent approach to design cloud solutions by addressing requirements across a pre-defined set of aspects and domains, which are technology-agnostic architectural areas that need to be considered for any enterprise solution. It can be used as a guide to make the necessary design and component choices to ensure you have considered applicable requirements for each aspect and domain. After you have identified the applicable requirements and domains that are in scope, you can evaluate and select the best fit for purpose components for your enterprise cloud solution.

The Figure 3 shows the domains that are covered in this solution.


## Solution components and requirements for {{site.data.keyword.satelliteshort}} location on-premises
{: #solution-components-on-prem}

Review the following requirements and components for configuring MAS in an on-premises {{site.data.keyword.satelliteshort}} location.

## Requirements <!-- H2 -->
{: #requirements}

<!-- insert the requirements table, below is an example -->

The following table represents a baseline set of requirements, which are applicable to many clients who are looking to migrate from Maximo 7.x to Maximo Application Suite (MAS) 8.x. Deployment of MAS on {{site.data.keyword.satellitelong_notm}} location serves as the first step.

| Aspect | Requirement |
|---|---|
| Compute | Customer is looking to deploy hosts running managed Red Hat OpenShift Kubernetes Service (ROKS) clusters in the {{site.data.keyword.satelliteshort}} location |
| Storage | Provide storage that meets the MAS applications and database performance requirements |
| Network | Provide secure, low-latency connectivity |
| Data | Data security and compliance requirements require that the data remain on-premises |
| Security | Encrypt all application data in transit and at rest to protect it from unauthorized disclosure. |
| Resiliency | - Multi-site capability to support a disaster recovery strategy and solution that uses {{site.data.keyword.Bluemix_notm}} infrastructure DR capabilities that are combined with {{site.data.keyword.satelliteshort}} features. \n - Provide backups for MAS data retention. |
| Service management | Customer wants a fully managed service |
| Other | Shorten the time required to migrate from Maximo 7.x to MAS 8.x |
| | Use a managed ROKS service since customer does not have the needed skills |
| | Provide an Image Replication migration solution that will minimize disruption during cut-over |
| | Access customer's existing Red Hat Container Registry |
| | Use multiple {{site.data.keyword.satelliteshort}} locations to enable DR for MAS applications |
{: caption="Table 1. Pattern requirements" caption-side="bottom"}  <!-- each table MUST have a caption attribute>

{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.satelliteshort}} is a fully managed offering and there are certain responsibilities that are shared by IBM and the customer. For more information about the table and the corresponding task details, see [{{site.data.keyword.satelliteshort}} responsibilities](/docs/satellite?topic=satellite-responsibilities).

## Components <!-- H2 -->
{: #components}

For a list of {{site.data.keyword.satelliteshort}}-related components please [see](https://cloud.ibm.com/docs/pattern-base-ibm-cloud-satellite)

| Aspect| Component| How the component is used |
|---|---|---|
| Cloud | {{site.data.keyword.satellitelong_notm}} | Distributed cloud paradigm |
| | Location infrastructure | On-premises: Client provided infrastructure |
| | Management plane MZR | Closest region (MZR) to {{site.data.keyword.satelliteshort}} location |
| Compute | {{site.data.keyword.satelliteshort}} location hosts | Virtual machine (VM) or {{site.data.keyword.baremetal_short_sing}} |
| | Host OS | RHEL 8.x or RHCOS |
| | Control plane hosts	| 4 vCPU and 16 GB RAM |
| | {{site.data.keyword.satelliteshort}} services worker nodes hosts: \n Red Hat OpenShift (Customer Workload Cluster) | - 16 vCPU and 64 GB RAM (minimum of 3spares) for Red Hat OpenShift Data Foundation persistent storage. \n - Regular nodes that are tailored to workload but can be as low as 4x16 |
| | {{site.data.keyword.satelliteshort}} services worker nodes hosts : \n Other {{site.data.keyword.satelliteshort}}-enabled services | Based on {{site.data.keyword.satelliteshort}}-enabled service. This reference solution does not include any other services. |
| | Containers | Managed Red Hat OpenShift on {{site.data.keyword.satelliteshort}} |
| | Red Hat OpenShift cluster connectivity | - Private Service cluster URL \n - Public Domain Name System (DNS) pointing to control plane node IPs by default \n - Private {{site.data.keyword.satelliteshort}} link endpoint for Red Hat OpenShift cluster accessible within {{site.data.keyword.Bluemix_notm}} private network  |
| | Workloads Access | - Red Hat OpenShift Routes \n - Node Ports \n - There is the ability to integrate external load balancers, just point load balancer to the Red Hat OpenShift router node port. {: note} |
| | Workload isolation | Single cluster for all workloads |
| | Container Images Registry | {{site.data.keyword.registrylong_notm}} on {{site.data.keyword.Bluemix_notm}} |
| Storage: Primary | {{site.data.keyword.satelliteshort}} Hosts: Control plane and worker nodes host node local storage
| | {{site.data.keyword.satelliteshort}} Services storage: \n Red Hat OpenShift (Customer Workloads) | Software Defined Storage (SDS) |
| | Software Defined Storage | - Red Hat OpenShift Data Foundation\n - Portworx enterprise (if customer is an existing Portworx user) |
| | Portworx enterprise storage | Worker node host local disks |
| | {{site.data.keyword.satelliteshort}} services storage template: \n Red Hat OpenShift | Bring your Own Driver: Portworx |
| | {{site.data.keyword.satelliteshort}} Services Storage Template: \n Other {{site.data.keyword.satelliteshort}} enabled services | Based on {{site.data.keyword.satelliteshort}} enabled service |
| | | |
| Storage: Backup | {{site.data.keyword.satelliteshort}} Control Plane Data | {{site.data.keyword.cos_full_notm}} (IBM-managed backups) |
| | Red Hat OpenShift workload data | Customer might choose to use Cloud Object Storage on {{site.data.keyword.Bluemix_notm}} |
| Networking |Enterprise Connectivity | |
| | {{site.data.keyword.satelliteshort}} location and {{site.data.keyword.dl_full_notm}} 2.0 connect or internet |
| | {{site.data.keyword.satelliteshort}} location private Network | VPN or Use {{site.data.keyword.satelliteshort}} link for Transmission Control Protocol (TCP) and HTTPS connections (no User Datagram Protocol)|
| | Cloud Connectivity | |
| | {{site.data.keyword.satelliteshort}} location connectivity | {{site.data.keyword.satelliteshort}} link over public network
| | {{site.data.keyword.satelliteshort}} Services Connectivity | {{site.data.keyword.satelliteshort}} link location endpoint for Red Hat OpenShift cluster
| | {{site.data.keyword.Bluemix_notm}} services connectivity | {{site.data.keyword.satelliteshort}} link cloud endpoints
| | Load balancers | |
| | Red Hat OpenShift application load balancer | 3rd party load balancer –Ingress Controller |
| | Segmentation | |
| | Red Hat OpenShift cluster | Container network policies |
| | DNS | Client DNS at {{site.data.keyword.satelliteshort}} location |
| Security: Data | | |
| Data encryption at rest | {{site.data.keyword.satelliteshort}} control plane backup storage | Cloud Object Storage encrypted with provider keys |
| | {{site.data.keyword.satelliteshort}} worker nodes data | Worker nodes storage encryption: Customer |
| | Red Hat OpenShift cluster persistent storage | Cluster volume encryption with Kubernetes Secret |
| Data encyption in transit | {{site.data.keyword.satelliteshort}} Link | Encryption that uses TLS |
| | Red Hat OpenShift cluster workloads | App-level encryption that uses TLS |
| | Certificate Lifecycle Management | Customer on-premises certificate manager |
| Security: Identity and Access Management (IAM) | | |
| IAM: Access & Role Management |	{{site.data.keyword.satelliteshort}} Location | - {{site.data.keyword.Bluemix_notm}} account set up \n - Account and Resource Organization \n - {{site.data.keyword.Bluemix_notm}} IAM roles and access groups |
| | {{site.data.keyword.satelliteshort}} location hosts | {{site.data.keyword.Bluemix_notm}} IAM | |
| | {{site.data.keyword.satelliteshort}} services: \n Red Hat OpenShift (Customer Workloads Cluster) | - {{site.data.keyword.Bluemix_notm}} IAM Roles \n - Kubernetes role-based access control (RBAC) Roles |
| IAM: Application | Runtime security (WAF and DDoS) | Bring your own Edge Security | |
| IAM: Infrastructure & endpoint | Core Network Protection | Subnets and firewall rules | |
| IAM: Threat detection and response | Threat detection | Customer SIEM tool, for example, Splunk | |
| Resiliency: High availability | {{site.data.keyword.satelliteshort}} Host Nodes (control and worker nodes) | Multi-zone deployment | |
| | Red Hat OpenShift workloads | Multi-zone Red Hat OpenShift cluster | |
| Resiliency: Backup | Red Hat OpenShift clusters | Portworx PX Backup for Kubernetes | |
| Service management: Monitoring | {{site.data.keyword.satelliteshort}} location and hosts | - IBM {{site.data.keyword.satelliteshort}} Monitoring Tool \n - {{site.data.keyword.monitoringlong_notm}} | |
| | Red Hat OpenShift clusters | {{site.data.keyword.monitoringlong_notm}} | |
| Service management: Logging | {{site.data.keyword.satelliteshort}} location and hosts | - IBM {{site.data.keyword.satelliteshort}} {{site.data.keyword.loganalysisshort}} tool \n - {{site.data.keyword.loganalysislong}} |
| | Red Hat OpenShift clusters | {{site.data.keyword.loganalysislong_notm}} |
| Service management: Auditing | {{site.data.keyword.satelliteshort}}e location events | {{site.data.keyword.cloudaccesstraillong}} |
| | Red Hat OpenShift clusters | {{site.data.keyword.cloudaccesstraillong}} |
{: caption="Table 2. Pattern components" caption-side="bottom"} <!-- each table MUST have a caption attribute>

As mentioned earlier, the Architecture Framework is used to guide and determine the applicable aspects and domains for which architecture decisions need to be made. The following sections contain the considerations, and architecture decisions for the aspects and domains that are in play in this solution pattern.
