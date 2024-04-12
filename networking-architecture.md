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
{: #enterprise-connectivity}

The following are architecture decisions for enterprise connectivity for this design.

| Architecture decision | Requirement | Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Management connectivity | Provide secure, encrypted connectivity to the cloud’s private network for management purposes. | text | text | text. |
| Enterprise connectivity | Provide connectivity between client enterprise and IBM Cloud. | text | text | text. |
{: caption="Table 1. Architecture decisions for enterprise connectivity" caption-side="bottom"}

## Architecture decisions for BYOIP and Edge Gateways
{: #byoip-edge-gateways}

The following are network BYOIP and edge gateay architecture decisions for this design.

| Architecture decision | Requirement | Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| BYOIP approach | Provide capability for bring your own IP (BYOIP) to IBM Cloud. | text | text | text |
| Edge gateways | Capability to provide edge routing services and possible tunnel termination. | text | text | text |
{: caption="Table 2. Architecture decisions for bring your own IP and edge gateways" caption-side="bottom"}

## Architecture decisions for network segmentation and isolation
{: #network-segmentation-isolation}

The following are network segmentation and isolation architecture decisions for this design.

| Architecture decision | Requirement | Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Network segmentation and isolation | Ability to provide network isolation across workloads. | text | text | text |
{: caption="Table 3. Architecture decisions for network segmentation and isolation" caption-side="bottom"}

## Architecture decisions for cloud native connectivity
{: #cloud-native-connectivity}

The following are cloud native connectivity architecture decisions for this design.

| Architecture decision | Requirement | Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Cloud native connectivity (to cloud services) | Provide secure connection to Cloud Services | * VPC Gateway + Virtual Private Endpoints (VPE) \n * Private Cloud Service endpoints \n * Public Cloud Service Endpoints | text | text |
| Multi-landing zone connectivity | Connect two or more VPCs over a private network /n Connectectivity between classic, VPCs and/or Power Virutal Server| * Global Transit Gateway \n * Local Transit Gateway (TGW) | text | text |
{: caption="Table 4. Architecture decisions for cloud native connectivity" caption-side="bottom"}

## Architecture decisions for load balancing
{: #network-load-balancing}

The following are load balancing architecture decisions for this design.

| Architecture decision | Requirement | Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Global load balancing | Load balancing over the public network across two regions in the event of an outage (DR) for failover to the other region. | text | text |text|
| Load balancing (public) | Load balancing workloads across multiple workload instances or zones over the public network. | text | text |text|
| Load balancing (private) | Load balancing workloads across multiple workload instances or zones over the private network. | Dedicated VM \n  Commercial LB | Dedicated VM | Recommend using a dedicated VM for load balancing. If already availabe, use a commercial grade L4 load balancer, such as NGINX, F5, or other load balancer.|
{: caption="Table 5. Architecture decisions for load balancing" caption-side="bottom"}

## Architecture decisions for content delivery network
{: #network-content delivery network}

The following are content delivery network architecture decisions for this design.

| Architecture decision | Requirement | Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Content delivery network | Provide ability to cache frequently accessed content at location nearest to the user | text | text | text |
{: caption="Table 6. Architecture decisions for content delivery network" caption-side="bottom"}


## Architecture decisions for domain name system
{: #dns}

The following are domain name system (DNS) architecture decisions for this design.

| Architecture decision | Requirement | Option | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Public DNS | Provide DNS resolution to support the use of hostnames instead of IP addresses for applications | text | text | text |
| Private DNS | Provide DNS resolution within IBM Cloud's private network | text| text | text |
{: caption="Table 7. Architecture decisions for domain name system" caption-side="bottom"}

## Architecture decisions for enterprise connectivity in Satellite
{: #enterprise-connectivity-sat}


| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Network connectivity | Connectivity between {{site.data.keyword.satelliteshort}} Location and {{site.data.keyword.Bluemix_notm}}  | - {{site.data.keyword.satelliteshort}} link \n - Public network \n - Direct link | {{site.data.keyword.satelliteshort}} link over public network | {{site.data.keyword.satelliteshort}} link proxies network traffic over a secure TLS connection between cloud services and resources in the {{site.data.keyword.satelliteshort}} location. This link tunnel serves as a communication path over the internet that uses the Transmission Control Protocol (TCP) and port 443. This is the default configuration. |
| | {{site.data.keyword.satelliteshort}} location that uses private network | Virtual Private Network (VPN) | VPN | VPN connection to the {{site.data.keyword.satelliteshort}} location private network is needed to access {{site.data.keyword.satelliteshort}} location resources and services, for example, the Red Hat OpenShift console that's not exposed to the public network. |
| | Cloud connectivity to {{site.data.keyword.satelliteshort}} enabled services \n Red Hat OpenShift (Customer workloads) | {{site.data.keyword.satelliteshort}} link location endpoint | {{site.data.keyword.satelliteshort}} link location endpoint | {{site.data.keyword.satelliteshort}} link Location endpoints provide access to {{site.data.keyword.satelliteshort}} location resources and services from within the {{site.data.keyword.Bluemix_notm}} private network. \n By default, {{site.data.keyword.satellitelong_notm}} creates a {{site.data.keyword.satelliteshort}} link location endpoint to access the Red Hat OpenShift cluster that runs in the location. This endpoint can be optionally enabled to allow the cluster to be managed through a {{site.data.keyword.satelliteshort}} configuration. |
{: caption="Table 1. Architecture decisions for enterprise connectivity" caption-side="bottom"}



## Architecture decisions for network segmentation and isolation
{: #network-segmentation-isolation-sat}


| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Network segmentation | Network segmentation and isolation | - [Container network policies](/docs/openshift?topic=openshift-network_policies) \n - Red Hat OpenShift service mesh | Container network policies | Container network policies restrict egress and ingress traffic and communication between applications. \n - Allow or block network traffic on specific network interfaces regardless of the Kubernetes pod source or destination IP address or Classless Inter-Domain Routing (CIDR). \n - Allow or block network traffic for pods across namespaces. For more information, see [Overview of network security options](/docs/openshift?topic=openshift-network_policies). |
{: caption="Table 2. Architecture decisions for network segmentation and isolation" caption-side="bottom"}



## Architecture decisions for load balancing
{: #network-load-balancing-sat}


| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
|Load Balancing | Application Load Balancer (ALB) | - 3rd party load balancer: Ingress controller \n - External load balancer in cloud provider | 3rd party load balancer: Ingress controller  | Use a [third-party load balancer and Red Hat OpenShift routes](/docs/openshift?topic=openshift-sat-expose-apps) to expose apps with a hostname and add health checking for the host IP addresses that are registered in the router's Domain Name System (DNS) records. As an example, [MetalLB](https://metallb.universe.tf/){: external} can be deployed on Red Hat OpenShift cluster worker nodes that are dedicated to the Ingress controller. |
{: caption="Table 3. Architecture decisions for load balancing" caption-side="bottom"}



## Architecture decisions for domain name system
{: #dns-sat}


| Architecture decision | Requirement | Option | Decision | Rationale |
|---|---|---|---|---|
| Domain Name System (DNS) | Public DNS | - Client DNS at {{site.data.keyword.satelliteshort}} location \n -  Cloud Internet Services (CIS) | Client DNS at {{site.data.keyword.satelliteshort}} location | Provides consistent DNS across {{site.data.keyword.satelliteshort}} location private cloud to support custom DNS domains instead of DNS domains provided by default. |
{: caption="Table 4. Architecture decisions for domain name system" caption-side="bottom"}
