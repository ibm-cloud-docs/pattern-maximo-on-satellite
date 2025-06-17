---

copyright:
  years: 2024
lastupdated: "2025-06-17"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

---

{{site.data.keyword.attribute-definition-list}}

# Architecture decisions for networking
{: #networking-architecture}

There are 2 sets of architectural decisions in this pattern, one pertains to {{site.data.keyword.satellitelong_notm}} and the other to {{site.data.keyword.prodname_imas_full_notm}}.

## Architecture decisions for enterprise connectivity in {{site.data.keyword.prodname_imas_short}}
{: #enterprise-connectivity-mas}

The following are architecture decisions about networking for {{site.data.keyword.prodname_imas_full_notm}}.

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Enterprise connectivity | High-speed connectivity | - Direct Link 2.0 \n  - VPN Gateway | Direct Link 2.0 | Provides private links that are [dedicated or multi-tenant](/docs/dl/getting-started#get-started-with-direct-link-connect) and doesn't expose any traffic to the public network. The preferred option for regulated workloads with strict network isolation requirements  \n  - [Satellite Link](/docs/satellite?topic=satellite-link-location-cloud) can offer a secure connection over Direct Link |
{: caption="Architecture decisions for enterprise connectivity in {{site.data.keyword.prodname_imas_short}}" caption-side="bottom"}


## Architecture decisions for network segmentation and isolation in {{site.data.keyword.prodname_imas_short}}
{: #network-segmentation-isolation-mas}

The following are network segmentation and isolation architecture decisions for this design.

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Network segmentation and isolation | Ability to provide network isolation | - VPCs \n - Subnets \n  - Security groups \n Access Control Lists (ACLs) \n [Container network policies](/docs/openshift?topic=openshift-network_policies) | Subnets, security Groups, Access Control Lists, container network policies available in the {{site.data.keyword.satelliteshort}} location | Security groups define groups of resources, which might be in different subnets and assign uniform access rules to them. Security groups can be used as virtual firewalls to control traffic flow to and from worker nodes. \n ACLs define a list of rules that limit who can access a subnet within a VPC. ACLs can be used to control traffic flow to and from the Red Hat OpenShift cluster subnets. \n Container network policies restrict egress and ingress traffic and communication between applications. |
| Firewall protection | Firewall (FW) | Juniper vSRX \n Palo Alto \n Fortigate | Juniper vSRX | Customer to provide FW license or have IBM provide it |
{: caption="Architecture decisions for network segmentation and isolation in {{site.data.keyword.prodname_imas_short}}" caption-side="bottom"}


## Architecture decisions for load balancing in {{site.data.keyword.prodname_imas_short}}
{: #network-load-balancing-mas}

The following are load balancing architecture decisions for this design.

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Global load balancing | Load balancing over the public network across two regions if an outage occurs, disaster recovery, for failover to the other region. | Global load balancer (GLB) on-premises \n {{site.data.keyword.Bluemix_notm}} DNS Services | Global load balancer on-premises | The [Global load balancer](/docs/dns-svcs?topic=dns-svcs-global-load-balancers) on-premises distributes the traffic for apps that are accessed through the enterprise network. \n The {{site.data.keyword.Bluemix_notm}} DNS Services can be used |
| Load balancing (private) | Load balancing workloads across multiple workload instances over the private network. | Dedicated VM \n Commercial load balancer | Dedicated VM | It's recommended to use a dedicated VM for load balancing. If already available, use a commercial grade L4 load balancer, such as NGINX, F5, or other load balancer. |
{: caption="Architecture decisions for load balancing in {{site.data.keyword.prodname_imas_short}}" caption-side="bottom"}


## Architecture decisions for enterprise connectivity in Satellite
{: #enterprise-connectivity-sat}

The following are architecture decisions about networking for {{site.data.keyword.satellitelong_notm}}.

| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Network connectivity | Connectivity between {{site.data.keyword.satelliteshort}} location and {{site.data.keyword.Bluemix_notm}}  | - {{site.data.keyword.satelliteshort}} link \n - Public network \n - Direct link | {{site.data.keyword.satelliteshort}} link over public network | {{site.data.keyword.satelliteshort}} link proxies network traffic over a secure TLS connection between cloud services and resources in the {{site.data.keyword.satelliteshort}} location. This link tunnel serves as a communication path over the internet that uses the Transmission Control Protocol (TCP) and port 443. This is the default configuration. |
| | {{site.data.keyword.satelliteshort}} location that uses private network | Virtual Private Network (VPN) | VPN | VPN connection to the {{site.data.keyword.satelliteshort}} location private network is needed to access {{site.data.keyword.satelliteshort}} location resources and services, for example, the Red Hat OpenShift console that's not exposed to the public network. |
| | Cloud connectivity to {{site.data.keyword.satelliteshort}} enabled services \n Red Hat OpenShift: Customer workloads | {{site.data.keyword.satelliteshort}} link location endpoint | {{site.data.keyword.satelliteshort}} link location endpoint | {{site.data.keyword.satelliteshort}} link Location endpoints provide access to {{site.data.keyword.satelliteshort}} location resources and services from within the {{site.data.keyword.Bluemix_notm}} private network. \n By default, {{site.data.keyword.satellitelong_notm}} creates a {{site.data.keyword.satelliteshort}} link location endpoint to access the Red Hat OpenShift cluster that runs in the location. This endpoint can be optionally enabled to allow the cluster to be managed through a {{site.data.keyword.satelliteshort}} configuration. |
{: caption="Architecture decisions for enterprise connectivity in {{site.data.keyword.satellitelong_notm}}" caption-side="bottom"}

## Architecture decisions for network segmentation and isolation in Satellite
{: #network-segmentation-isolation-sat}


| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Network segmentation | Network segmentation and isolation | - [Container network policies](/docs/openshift?topic=openshift-network_policies) \n - Red Hat OpenShift service mesh | Container network policies | Container network policies restrict egress and ingress traffic and communication between applications. \n - Allow or block network traffic on specific network interfaces regardless of the Kubernetes pod source or destination IP address or Classless Inter-Domain Routing (CIDR). \n - Allow or block network traffic for pods across namespaces. For more information, see [Overview of network security options](/docs/openshift?topic=openshift-network_policies). |
{: caption="Architecture decisions for network segmentation and isolation in {{site.data.keyword.satellitelong_notm}}" caption-side="bottom"}


## Architecture decisions for load balancing in Satellite
{: #network-load-balancing-sat}


| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
|Load Balancing | Application Load Balancer (ALB) | - 3rd party load balancer: Ingress controller \n - External load balancer in cloud provider | 3rd party load balancer: Ingress controller  | Use a [third-party load balancer and Red Hat OpenShift routes](/docs/openshift?topic=openshift-sat-expose-apps) to expose apps with a hostname and add health checking for the host IP addresses that are registered in the routers Domain Name System (DNS) records. As an example, [MetalLB](https://metallb.universe.tf/){: external} can be deployed on Red Hat OpenShift cluster worker nodes that are dedicated to the ingress controller. |
{: caption="Architecture decisions for load balancing in {{site.data.keyword.satellitelong_notm}}" caption-side="bottom"}



## Architecture decisions for domain name system in Satellite
{: #dns-sat}


| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Domain Name System (DNS) | Public DNS | - Client DNS at {{site.data.keyword.satelliteshort}} location \n - {{site.data.keyword.cis_short}} | Client DNS at {{site.data.keyword.satelliteshort}} location | Provides consistent DNS across {{site.data.keyword.satelliteshort}} location private cloud to support custom DNS domains instead of DNS domains provided by default. |
{: caption="Architecture decisions for domain name system in {{site.data.keyword.satellitelong_notm}}" caption-side="bottom"}
