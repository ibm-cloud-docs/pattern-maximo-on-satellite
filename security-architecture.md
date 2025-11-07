---

copyright:
  years: 2024
lastupdated: "2025-06-17"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

---

# Architecture decisions for security
{: #security-architecture}

There are 2 sets of architectural decisions in this pattern, one pertains to {{site.data.keyword.satellitelong_notm}} and the other to {{site.data.keyword.prodname_imas_full_notm}}.


## Architecture decisions for data security: Encryption in {{site.data.keyword.prodname_imas_short}}
{: #data-encryption-mas}

The following are architecture decisions about security for {{site.data.keyword.prodname_imas_full_notm}}.

| Architecture decision | Requirement |  Option | Decision | Rationale |
|---|---|---|---|---|
| Encryption of databases | Encrypt data in database to protect it from unauthorized disclosure | - Use system-generated values  \n - Bring Your Own encryption keys | Use system-generated values | Encryption keys and encryption algorithms are specified when configuring {{site.data.keyword.prodname_imas_full_notm}} Manage. Choose the fields that require [security](https://www.ibm.com/docs/en/masv-and-l/cd?topic=encryption-database-overview){: external}. The secret is automatically generated. |
| Data encryption of backups | Encrypt and compress backup data to protect it from unauthorized access | - Use *tar* command  n\ - Bring Your Own encryption tool and service | Bring Your Own encryption tool and service | The admin can run the *tar* [command](https://www.ibm.com/docs/en/masv-and-l/cd?topic=procedures-encrypting-compressing-backups){: external}. Remember to decrypt when restoring data from backup. |
| Data encryption of logs | Encrypt all operational and audit logs at rest to protect them from unauthorized disclosure. | Bring Your Own encryption tool and service | Bring Your Own encryption tool and service |  |
{: caption="Data encryption architecture decisions for {{site.data.keyword.prodname_imas_short}}" caption-side="bottom"}

## Architecture decisions for data security: Key management in {{site.data.keyword.prodname_imas_short}}
{: #kms-mas}

| Architecture decision | Requirement |  Option | Decision | Rationale |
|---|---|---|---|---|
| Key lifecycle management and hardware security modules | Encrypt data at rest and in transit by using customer-managed keys to protect them from unauthorized access.  | Key Protect \n Hyper Protect Crypto Services (HPCS) | Key Protect | Key Protect is recommended for applications that need to comply with regulations requiring encryption of data with customer-managed keys. Key Protect provides key management services by using a shared multi-tenant FIPS 140-2 Level 3 certified hardware security modules. |
| Certificate management | Manage and deploy SSL/TLS certificates for Maximo apps | IBM Certificate Manager \n Bring Your Own Certificate Manager | IBM Certificate Manager | IBM Certificate Manager controls certificate management in {{site.data.keyword.prodname_imas_full_notm}} 8.8 and above. It is automatically installed as part of {{site.data.keyword.prodname_imas_full_notm}} [installation](https://www.ibm.com/docs/en/masv-and-l/cd?topic=installing){: external}. |
{: caption="Key management architecture decisions for {{site.data.keyword.prodname_imas_short}}" caption-side="bottom"}

## Architecture decisions for identity and access management in {{site.data.keyword.prodname_imas_short}}
{: #iam-mas}

| Architecture decision | Requirement |  Option | Decision | Rationale |
|---|---|---|---|---|
| Identity & access management (IAM) | Administer users | - Local users  \n - Lightweight Directory Access Protocol (LDAP) users  \n - External users | Local users | {{site.data.keyword.prodname_imas_full_notm}} user records are stored in the MongoDB core database. For more information, see [Administering users and user access](https://www.ibm.com/docs/en/masv-and-l/cd?topic=administering-users-user-access){: external}. |
| IAM | Use a method to authenticate users | - Local authentication  \n - LDAP authentication  \n - Security Assertion Markup Language (SAML) authentication | Local authentication | With local authentication, {{site.data.keyword.prodname_imas_full_notm}} provides single sign-on (SSO) for all fully integrated applications. For more information, see [Authentication methods](https://www.ibm.com/docs/en/masv-and-l/cd?topic=authentication-methods){: external}. |
| IAM | Securely authenticate users for platform services and control access to resources consistently across {{site.data.keyword.Bluemix_notm}} | {{site.data.keyword.Bluemix_notm}} IAM | {{site.data.keyword.Bluemix_notm}} IAM | Create {{site.data.keyword.Bluemix_notm}} Account then use IAM access policies to assign users, service IDs, and trusted profiles access to resources within the {{site.data.keyword.Bluemix_notm}} account. For more information, see [Creating your IBM Cloud account and configuring permissions](https://www.ibm.com/docs/en/masv-and-l/cd?topic=cloud-creating-your-account-configuring-permissions){: external}.|
| Privileged access management | Ensure that all operator actions are run securely through a bastion host | Bastion Host | Bastion Host | Bastion Host VM is used to provision the OCP bootstrap node. It is provisioned through SSH over a private network to securely access resources within {{site.data.keyword.Bluemix_notm}}’s private network. For more information, see [Maximo Application Suite on-premises installation topologye](https://www.ibm.com/docs/en/masv-and-l/cd?topic=premises-installation-topology){: external}. |
{: caption="Identity and access management architecture decisions for {{site.data.keyword.prodname_imas_short}}" caption-side="bottom"}

## Architecture decisions for application security in {{site.data.keyword.prodname_imas_short}}
{: #app-security-mas}

| Architecture decision | Requirement |  Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| DDoS | - Enforce information flow policies and protect the boundaries of the application. \n - Protect against or limit the effects of denial-of-service attacks. | {{site.data.keyword.Bluemix_notm}} Internet Services (CIS) | IBM CIS | IBM CIS provide DDoS protection if exposed to the public network. For more information, see [Installing Cloud Internet Services](https://www.ibm.com/docs/en/masv-and-l/cd?topic=services-cloud-internet){: external}. |
{: caption="Application security architecture decisions for {{site.data.keyword.prodname_imas_full_notm}}" caption-side="bottom"}


## Architecture decisions for license management in {{site.data.keyword.prodname_imas_short}}
{: #license-management-mas}

| Architecture decision | Requirement |  Option | Decision | Rationale |
|---|---|---|---|---|
| License management | Manage virtualized environments and measure license utilization | Suite License Service (SLS) | SLS | The Suite License Service (SLS) stores and manages the Maximo® Application Suite license. The license file is uploaded to the SLS server as part of initial setup. For more information, see [Suite License Service](https://www.ibm.com/docs/en/masv-and-l/cd?topic=services-suite-license-service){: external}. |
| Administering licenses | Administer licenses and AppPoint usage | - Customer managed \n - IBM managed | IBM managed | IBM managed is handled by {{site.data.keyword.prodname_imas_full_notm}} representative. For more information, see [customer-managed](https://www.ibm.com/docs/en/masv-and-l/cd?topic=administering-licenses-apppoints-usage){: external}. |
{: caption="License management architecture decisions for {{site.data.keyword.prodname_imas_short}}" caption-side="bottom"}


The following sections summarize the security architecture decisions for the {{site.data.keyword.satellitelong_notm}} on-premises location.

## Architecture decisions for data encryption in Satellite
{: #data-encryption-sat}

The following are architecture decisions about security for {{site.data.keyword.satellitelong_notm}}.

| Architecture decision | Requirement |  Option | Decision | Rationale |
|---|---|---|---|---|
| Data encryption | - Encryption at rest \n - {{site.data.keyword.satelliteshort}} worker nodes data	| Worker nodes storage encryption: Customer | Worker nodes storage encryption: Customer	| The customer is responsible for encrypting the boot disk and any additional disks that you add to the {{site.data.keyword.satelliteshort}} worker nodes hosts to keep data secure and meet regulatory requirements. |
| | Encryption at rest \n Red Hat OpenShift persistent storage | - Backing-storage device encryption \n Cluster volume encryption with Kubernetes Secret \n {{site.data.keyword.keymanagementservicelong}} \n Bring your own Hardware Security Module (HSM) | Cluster volume encryption with Kubernetes Secret | - The customer is responsible for encrypting persistent storage by configuring storage device encryption or cluster encryption, if supported by the storage provider. \n In this solution, Portworx is used to provide persistent storage for Red Hat OpenShift cluster workloads. \n - Example Portworx set up: volume encryption with customers keys stored in Kubernetes Secret to encrypt data in transit and at rest. \n - Add Kubernetes Secret encryption |
| | Encryption at rest and in transit \n Backup storage	| - {{site.data.keyword.cos_full_notm}} encrypted with provider keys \n {{site.data.keyword.cos_full_notm}} encrypted with Key Management Service (KMS) | {{site.data.keyword.cos_full_notm}} encrypted with provider keys	|  {{site.data.keyword.IBM_notm}}-managed backups of the {{site.data.keyword.satelliteshort}} location control plane data are stored in customer created {{site.data.keyword.cos_full_notm}} buckets. Customer can select to encrypt {{site.data.keyword.cos_full_notm}} bucket with {{site.data.keyword.Bluemix_notm}} keys or KMS (Key Protect or Hyper Protect Crypto Services) created in {{site.data.keyword.Bluemix_notm}} MZR used to manage {{site.data.keyword.satelliteshort}}. In this solution, the customer {{site.data.keyword.cos_full_notm}} bucket is encrypted with {{site.data.keyword.Bluemix_notm}} keys. |
| | Encryption in transit \n {{site.data.keyword.satelliteshort}} link	| {{site.data.keyword.satelliteshort}} link encryption	| {{site.data.keyword.satelliteshort}} Link encryption	| All data that is transported over {{site.data.keyword.satelliteshort}} link is encrypted by using TLS 1.3 standards. This level of encryption is managed by {{site.data.keyword.IBM_notm}}. |
| | Encryption in transit \n Red Hat OpenShift cluster workloads | App level encryption that uses TLS \n Red Hat OpenShift service mesh | App-level encryption that uses TLS | Encryption in transit of application data is the customer’s responsibility. Applications can encrypt data by using TLS 1.2 at a minimum. |
| Certificates | Certificate lifecycle management | - Secrets Manager on {{site.data.keyword.Bluemix_notm}} \n Bring your own certificates | Bring your own certificates | The customer is responsible for providing and managing TLS certificates that are used for encrypting communication for workloads that are deployed on {{site.data.keyword.satelliteshort}} clusters. |
{: caption="Data encryption architecture decisions for Satellite" caption-side="bottom"}


## Architecture decisions for identity and access management in Satellite
{: #iam-sat}

| Architecture decision | Requirement |  Option | Decision | Rationale |
|---|---|---|---|---|
| {{site.data.keyword.iamlong}} (IAM) | {{site.data.keyword.satelliteshort}} location hosts | {{site.data.keyword.iamshort}} | {{site.data.keyword.iamshort}}  | After a host is assigned to a {{site.data.keyword.satelliteshort}} location, root SSH access is disabled (per CIS benchmark) and access to the host is controlled by [IAM access](/docs/openshift?topic=openshift-iam-platform-access-roles) |
|  | {{site.data.keyword.satelliteshort}} location | - {{site.data.keyword.Bluemix_notm}} account setup \n Account and resource organization \n {{site.data.keyword.Bluemix_notm}} IAM roles and access groups | - {{site.data.keyword.Bluemix_notm}} account setup \n Account and resource organization \n {{site.data.keyword.Bluemix_notm}} IAM roles and access groups | Account structure and access management with IAM role-based access control  enables zero trust through separation of duty and least privileged access. \n For more information, see [Account and resource organization](/docs/satellite?topic=satellite-iam-assign-access) and [{{site.data.keyword.Bluemix_notm}} IAM roles and access groups](/docs/satellite?topic=satellite-iam-platform-access). \n [{{site.data.keyword.satellitelong_notm}} platform and service access roles](/docs/satellite?topic=satellite-iam) in IAM are used to authenticate requests to the service and authorize user actions. |
|  | Red Hat OpenShift clusters | - [IAM roles](/docs/openshift?topic=openshift-iam-platform-access-roles) federated with a customer active directory \n [Kubernetes RBAC Roles](/docs/openshift?topic=openshift-iam-platform-access-roles) | - {{site.data.keyword.Bluemix_notm}} IAM roles \n Kubernetes role-based access control roles | - Red Hat OpenShift on {{site.data.keyword.Bluemix_notm}} uses IAM [platform and service access roles](/docs/openshift?topic=openshift-iam-platform-access-roles) to grant users access to the cluster \n - Role-based access control  roles and cluster roles define a set of permissions for how users can interact with Kubernetes resources in the cluster. - Role-based access control  roles can be applied to individual users, groups of users, or service accounts. For more granular access policies to perform specific Kubernetes actions, you can apply [custom RBAC policies](/docs/openshift?topic=openshift-iam-platform-access-roles). |
{: caption="Identity and access management architecture decisions for Satellite" caption-side="bottom"}

## Architecture decisions for application security in Satellite
{: #app-security-sat}

| Architecture decision | Requirement |  Option | Decision | Rationale |
|---|---|---|---|---|
| Application security | Enforce runtime security to protect against distributed denial-of-service (DDOS) attacks. | Bring your own edge security | Bring your own edge security | The customer is responsible for providing edge solution at {{site.data.keyword.satelliteshort}} location to protect {{site.data.keyword.prodname_imas_full_notm}} applications that are exposed to the public network. |
{: caption="Application security architecture decisions for Satellite" caption-side="bottom"}

Edge security generally protects against attacks and creates secure connections. It includes intrusion detection and prevention, URL and domain filtering, secure web gateway, zero trust network access (ZTNA), and other technologies, which help in isolating the {{site.data.keyword.satelliteshort}} location.

## Architecture decisions for infrastructure and endpoint in Satellite
{: #infrastructure-and-endpoint-sat}

| Architecture decision | Requirement |  Option | Decision | Rationale |
|---|---|---|---|---|
| Network protection | Core network protection |  Subnets and firewall rules | Subnets and firewall rules | The customer is responsible for setting up and managing physical and virtual networks, subnets, and firewalls rules at the {{site.data.keyword.satelliteshort}} location to meet security and regulatory requirements. |
{: caption="Infrastructure and endpoint architecture decisions for Satellite" caption-side="bottom"}

## Architecture decisions for threat detection and response in Satellite
{: #threat-detection-and-response-sat}

| Architecture decision | Requirement |  Option | Decision | Rationale |
|---|---|---|---|---|
| Threat detection and response (TDR) |  Identify and neutralize threats | Bring your own security information and event management (SIEM) tool, for example, Splunk. \n [IBM X-Force Threat Management](https://www.ibm.com/security/resources/security-threat-management?mhsrc=ibmsearch_a&mhq=X-Force%20Threate%20management){: external}. | Bring your own SIEM tool, for example, Splunk. | For hybrid cloud environments, customers typically prefer to use their current on-premises SIEM tools. |
{: caption="Threat detection and response architecture decisions for Satellite" caption-side="bottom"}
