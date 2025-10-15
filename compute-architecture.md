---

copyright:
  years: 2024
lastupdated: "2025-06-17"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

---

# Architecture decisions for compute
{: #compute}

There are 2 sets of architectural decisions in this pattern, one pertains to {{site.data.keyword.satellitelong_notm}} and the other to {{site.data.keyword.prodname_imas_full_notm}}.

## Architecture decisions for compute in {{site.data.keyword.prodname_imas_short}}
{: #compute-decisions-mas}

The following sections summarize the compute architecture decisions for the pattern that involves deployment of Maximo® Application Suite (MAS) on an {{site.data.keyword.satellitelong_notm}} on-premises location.


| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Compute: Hosts | Hosts to run Maximo | Virtual machine (VM) \n  {{site.data.keyword.baremetal_short}} | VM | Most MAS applications run on a set of VMs that comprise a Red Hat OpenShift cluster. These VMs have separate IP addresses and appear as nodes in the Red Hat OpenShift cluster. In this solution, the VMs are managed {{site.data.keyword.satelliteshort}} hosts deployed in an on-premises location. |
| | Operating System (OS) | Red Hat Enterprise Linux (RHEL) 8.x (min) \n RH Core OS | RHEL 8.x | Typically running x86 architecture. Bring Your Own RHEL license. For the latest specs, see [{{site.data.keyword.satelliteshort}} Host System Requirements](/docs/satellite?topic=satellite-host-reqs) |
| | RHOCP Control plane | 4 vCPU and 16 GB RAM \n  8 vCPU and 32 GB RAM \n  16 vCPU and 64 GB RAM \n  32 vCPU and 128 GB RAM | 8 vCPU and 32 GB RAM for Medium configuration | Minimum of 3 control nodes These control nodes also maintain an internal *etcd*  database that contains the Kubernetes resource definitions. See [etcd](/docs/containers?topic=containers-encryption)|
| Compute: Containers | Containers| Managed Red Hat OpenShift on {{site.data.keyword.satelliteshort}} \n  Kubernetes service | Managed Red Hat OpenShift on {{site.data.keyword.satelliteshort}} | Red Hat OpenShift on {{site.data.keyword.satellitelong_notm}} provides a managed container platform with automatic provisioning, backup and updates of control nodes and etcd storage. |
{: caption="Architecture decisions for compute related to {{site.data.keyword.prodname_imas_short}}" caption-side="bottom"}


## Architecture decisions for compute in Satellite
{: #compute-decisions-sat}

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Compute: Hosts | {{site.data.keyword.satelliteshort}} hosts | {{site.data.keyword.baremetal_short}} \n virtual machine (VM) | Virtual machine | {{site.data.keyword.satelliteshort}} hosts represent the compute machine on the selected infrastructure. In this solution, the {{site.data.keyword.satelliteshort}} hosts are virtual machines from an existing Kernel-based Virtual Machine or OpenStack environment that deploys at the customer’s on-premises locations. |
| | Host OS | RHEL 8.x (min) \n RH Core OS | RHEL 8.x | {{site.data.keyword.satelliteshort}} requires RHEL 7.x minimal image (no LAMP stack) on x86. Bring Your Own RHEL license. For the latest specs, see [{{site.data.keyword.satelliteshort}} Host System Requirements](/docs/satellite?topic=satellite-host-reqs) |
| | Control plane hosts | 4 vCPU and 16 GB RAM \n 16 vCPU and 64 GB RAM | 4 vCPU and 16 GB RAM | Minimum of 3 host nodes. Minimum of 6 hosts for RHCOS. Must be in multiples of 3, for example, 6, 9, 12. The configuration and number of control planes hosts that are needed depends on the number of clusters, for customer workloads and {{site.data.keyword.satelliteshort}}-enabled services, which are deployed at the {{site.data.keyword.satelliteshort}} location and the total number of worker nodes across all clusters. For more information, see [{{site.data.keyword.satelliteshort}} Location Sizing](/docs/satellite?topic=satellite-location-host)|
| | {{site.data.keyword.satelliteshort}} services worker node hosts: Red Hat OpenShift | 4 vCPU and 16 GB RAM \n 16 vCPU and 64 GB RAM | 16 vCPU and 64 GB RAM | A minimum of 3 host nodes and it's recommended to have spare nodes in multiples of 3, for example 6, 9, 12. A larger configuration is used in this solution to support converged compute and storage requirements. The number of worker node hosts depends on the customer workloads to be deployed in the clusters. For more information, see [Sizing your Red Hat OpenShift cluster to support your workload](/docs/openshift?topic=openshift-strategy). |
| | {{site.data.keyword.satelliteshort}} services worker nodes hosts: Other services | 4 vCPU and 16 GB RAM \n 16 vCPU and 64 GB RAM | For more information, see [{{site.data.keyword.satelliteshort}}-Enabled Services](/docs/satellite?topic=satellite-managed-services) | Review the requirements for each [Satellite-Enabled Service](/docs/satellite?topic=satellite-managed-services). |
| Compute: Containers | Compute: Containers| Managed Red Hat OpenShift on {{site.data.keyword.satelliteshort}} \n Bring Your Own Red Hat OpenShift on-premises | Managed Red Hat OpenShift on {{site.data.keyword.satelliteshort}} | Ease of provisioning and managed control plane \n Consistent deployment of Red Hat OpenShift clusters across customer locations |
| | Red Hat OpenShift Cluster: Container images registry | {{site.data.keyword.registrylong}} \n Red Hat OpenShift Container Registry \n Bring Your Own image registry | {{site.data.keyword.registryfull_notm}} | By default, the Red Hat OpenShift internal registry is disabled because it does not have backing storage. {{site.data.keyword.registryfull_notm}} is a highly available private registry that can be accessed from multiple clusters and provides vulnerability scanning of the images. |
| | Red Hat OpenShift cluster: Connectivity | Private service cluster URL \n Public service cluster URL | Private service cluster URL | By default, the Red Hat OpenShift cluster that runs in the location can be accessed through the service cluster URL from only the {{site.data.keyword.satelliteshort}} location’s private network. \n If the {{site.data.keyword.satelliteshort}} location hosts have public internet access, the service cluster URL can be updated to enable access to the cluster from the public network. This is not recommended for production workloads. For more information, see [Host Network Connectivity](/docs/openshift?topic=openshift-sat-expose-apps). |
| | Red Hat OpenShift cluster: Workloads access | Red Hat OpenShift routes \n Node ports | Red Hat OpenShift routes | Expose apps to requests from the public or a private network with a hostname from Red Hat OpenShift Ingress controller's external IP address. Support HTTP and HTTPS protocols only. If the worker node hosts have public network connectivity, the cluster is created with a public Ingress controller by default. If the worker node hosts have private network connectivity only, the cluster is created with a private Ingress controller by default. |
| | | | Node ports | Expose non-HTTP(S) apps, for example, User Datagram Protocol or Transmission Control Protocol (TCP) apps, with a NodePort in the 30000-32767 range. |
| | Red Hat OpenShift cluster: Workload isolation | Single cluster for all workloads \n Separate clusters per workload | Single cluster for all workloads | Single cluster for all workloads. Workload isolation is achieved through projects and namespaces within a cluster. For more information, see [Container network policies](/docs/openshift?topic=openshift-network_policies), and IAM access roles. |
{: caption="Architecture decisions for compute related to {{site.data.keyword.satellitelong_notm}}" caption-side="bottom"}
