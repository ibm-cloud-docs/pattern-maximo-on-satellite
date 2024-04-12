---

copyright:
  years: 2024
lastupdated: "2024-01-23"

subcollection: <repo-name>

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Architecture decisions for networking
{: #networking-architecture}



The following sections summarize the networking architecture decisions for the pattern that involves deployment of Maximo® Application Suite (MAS) on an {{site.data.keyword.satellitelong_notm}} on-premises location.

## Architecture decisions for enterprise connectivity in MAS
{: #enterprise-connectivity-mas}

The following are architecture decisions for enterprise connectivity for this design.

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Enterprise connectivity | Highspeed connectivity | Direct Link 2.0 \n  VPN Gateway | Direct Link 2.0 | Provides private links [dedicated or multi-tenant](https://cloud.ibm.com/docs/dl/getting-started#get-started-with-direct-link-connect) and does not expose any traffic to the public network. Preferred option for regulated workloads with strict network isolation requirements  \n  Note. [Satellite Link](https://cloud.ibm.com/docs/satellite?topic=satellite-link-location-cloud) can offer that secure connection over Direct Link |
{: caption="Table 1. Architecture decisions for enterprise connectivity" caption-side="bottom"}


## Architecture decisions for network segmentation and isolation in MAS
{: #network-segmentation-isolation-mas}

The following are network segmentation and isolation architecture decisions for this design.

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Network segmentation and isolation | Ability to provide network isolation | VPCs \n  Subnets \n  Security Groups \n  ACLs \n  [Container Network Policies](https://cloud.ibm.com/docs/openshift?topic=openshift-network_policies) | Subnets, Security Groups, ACLs, Container Network Policies available in the {{site.data.keyword.satelliteshort}} location | Security groups (SGs) define groups of resources (which may be in different subnets) and assign uniform access rules to them. SGs can be used as virtual firewalls to control traffic flow to/from worker nodes. \n  ACLs define a list of rules that limit who can access a subnet within a VPC. ACLs can be used to control traffic flow to and from the OpenShift cluster subnets. \n  Container network policies restrict egress/ingress traffic and communication between applications. |
| Firewall protection | Firewall | Juniper vSRX \n  Palo Alto \n  Fortigate | Juniper vSRX | Customer to provide FW license or have IBM provide it |
{: caption="Table 2. Architecture decisions for network segmentation and isolation" caption-side="bottom"}


## Architecture decisions for load balancing in MAS
{: #network-load-balancing-mas}

The following are load balancing architecture decisions for this design.

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Global load balancing | Load balancing over the public network across two regions in the event of an outage (DR) for failover to the other region. | Global Load Balancer (GLB) on-prem \n  IBM Cloud DNS Services | GLB on-prem | The [Global Load Balancer](https://cloud.ibm.com/docs/dns-svcs?topic=dns-svcs-global-load-balancers) on-prem distributes the traffic for apps accessed through the enterprise network. \n  Note: that the IBM Cloud DNS Services could be used |
| Load balancing (private) | Load balancing workloads across multiple workload instances over the private network. | Dedicated VM \n  Commercial LB | Dedicated VM | Recommend using a dedicated VM for load balancing. If already availabe, use a commercial grade L4 load balancer, such as NGINX, F5, or other load balancer. |
{: caption="Table 3. Architecture decisions for load balancing" caption-side="bottom"}


## Architecture decisions for enterprise connectivity in Satellite
{: #enterprise-connectivity-sat}


| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Network connectivity | Connectivity between {{site.data.keyword.satelliteshort}} Location and {{site.data.keyword.Bluemix_notm}}  | - {{site.data.keyword.satelliteshort}} link \n - Public network \n - Direct link | {{site.data.keyword.satelliteshort}} link over public network | {{site.data.keyword.satelliteshort}} link proxies network traffic over a secure TLS connection between cloud services and resources in the {{site.data.keyword.satelliteshort}} location. This link tunnel serves as a communication path over the internet that uses the Transmission Control Protocol (TCP) and port 443. This is the default configuration. |
| | {{site.data.keyword.satelliteshort}} location that uses private network | Virtual Private Network (VPN) | VPN | VPN connection to the {{site.data.keyword.satelliteshort}} location private network is needed to access {{site.data.keyword.satelliteshort}} location resources and services, for example, the Red Hat OpenShift console that's not exposed to the public network. |
| | Cloud connectivity to {{site.data.keyword.satelliteshort}} enabled services \n Red Hat OpenShift (Customer workloads) | {{site.data.keyword.satelliteshort}} link location endpoint | {{site.data.keyword.satelliteshort}} link location endpoint | {{site.data.keyword.satelliteshort}} link Location endpoints provide access to {{site.data.keyword.satelliteshort}} location resources and services from within the {{site.data.keyword.Bluemix_notm}} private network. \n By default, {{site.data.keyword.satellitelong_notm}} creates a {{site.data.keyword.satelliteshort}} link location endpoint to access the Red Hat OpenShift cluster that runs in the location. This endpoint can be optionally enabled to allow the cluster to be managed through a {{site.data.keyword.satelliteshort}} configuration. |
{: caption="Table 4. Architecture decisions for enterprise connectivity" caption-side="bottom"}



## Architecture decisions for network segmentation and isolation in Satellite
{: #network-segmentation-isolation-sat}


| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Network segmentation | Network segmentation and isolation | - [Container network policies](/docs/openshift?topic=openshift-network_policies) \n - Red Hat OpenShift service mesh | Container network policies | Container network policies restrict egress and ingress traffic and communication between applications. \n - Allow or block network traffic on specific network interfaces regardless of the Kubernetes pod source or destination IP address or Classless Inter-Domain Routing (CIDR). \n - Allow or block network traffic for pods across namespaces. For more information, see [Overview of network security options](/docs/openshift?topic=openshift-network_policies). |
{: caption="Table 5. Architecture decisions for network segmentation and isolation" caption-side="bottom"}



## Architecture decisions for load balancing in Satellite
{: #network-load-balancing-sat}


| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
|Load Balancing | Application Load Balancer (ALB) | - 3rd party load balancer: Ingress controller \n - External load balancer in cloud provider | 3rd party load balancer: Ingress controller  | Use a [third-party load balancer and Red Hat OpenShift routes](/docs/openshift?topic=openshift-sat-expose-apps) to expose apps with a hostname and add health checking for the host IP addresses that are registered in the router's Domain Name System (DNS) records. As an example, [MetalLB](https://metallb.universe.tf/){: external} can be deployed on Red Hat OpenShift cluster worker nodes that are dedicated to the Ingress controller. |
{: caption="Table 6. Architecture decisions for load balancing" caption-side="bottom"}



## Architecture decisions for domain name system in Satellite
{: #dns-sat}


| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Domain Name System (DNS) | Public DNS | - Client DNS at {{site.data.keyword.satelliteshort}} location \n -  Cloud Internet Services (CIS) | Client DNS at {{site.data.keyword.satelliteshort}} location | Provides consistent DNS across {{site.data.keyword.satelliteshort}} location private cloud to support custom DNS domains instead of DNS domains provided by default. |
{: caption="Table 7. Architecture decisions for domain name system" caption-side="bottom"}
