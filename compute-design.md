---

copyright:
  years: 2024
lastupdated: "2024-05-07"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

---

{{site.data.keyword.attribute-definition-list}}

# Compute design
{: #compute-design}

In this solution pattern, an on-premises {{site.data.keyword.satelliteshort}} location is used because existing Maximo customers might want to keep their data on-premises or might want an environment to test out the migration process. For the {{site.data.keyword.satelliteshort}} location, customers can bring their own on-premises hardware or purchase from {{site.data.keyword.IBM}} or {{site.data.keyword.IBM_notm}} partners.

The recommendation for Maximo® Application Suite workloads is to size Red Hat OpenShift Container Platform (RHOCP) compute nodes at 4 GB memory per CPU. The number of CPU per compute node depends on the number and size of Maximo application workloads. For more information, see [Sizing Red Hat OpenShift Container Platform compute nodes](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=pi-sizing-red-hat-openshift-container-platform-compute-nodes){: external}.

{{site.data.keyword.satellitelong_notm}} should satisfy the compute requirements for setting up IBM® Maximo® Application Suite (MAS) on-premises including Red Hat OpenShift cluster specifications.
