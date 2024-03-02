---

copyright:
  years: 2024
lastupdated: "2024-02-15"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

---

{{site.data.keyword.attribute-definition-list}}

# Compute design <!-- H1 -->
{: #compute-design}

In this solution pattern an on-premises {{site.data.keyword.satelliteshort}} location is used because existing Maximo customers would want to keep their data on-premises or might want an environment to test out the migration process. For the {{site.data.keyword.satelliteshort}} location, customers can bring their own on-premises hardware or purchase from {{site.data.keyword.IBM}} or {{site.data.keyword.IBM_notm}} partners.

The recommendation for Maximo® Application Suite workloads, is to size Red Hat® OpenShift® Container Platform (RHOCP) compute nodes at 4 GB memory per CPU. And the number of CPU per compute node depend on the number and size of Maximo application workloads. Sizing details can be found [here](https://www.ibm.com/docs/en/mas-cd/continuous-delivery?topic=pi-sizing-red-hat-openshift-container-platform-compute-nodes)

{{site.data.keyword.satellitelong_notm}} should satisfy all of the compute requirements for setting up IBM® Maximo® Application Suite (MAS) on-premises including Red Hat OpenShift cluster specifications.
