---

copyright:
  years: 2024
lastupdated: "2024-01-23"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

---

{{site.data.keyword.attribute-definition-list}}

# Pre-certification scope
{: #pre-certification-questions}

There are many questions that need to asked during certification that are meant to help the solution team. They ought to be used as a checklist. All questions are not relevant to every solution or deal.


The aspects in the [architecture framework](/docs/architecture-framework?topic=architecture-framework-intro) are broadly used to classify the questions.

- **General:** DOUs, Day 2 team and responsibilities
- **Platform:** Classic, VPC, VMware
- **Storage:** Primary Storage, Backup Storage
- **Networking:** Enterprise Connectivity, Network Segmentation
- **Data:** Data Storage and security
- **Security:** Identity and Access Management, Infrastructure and Endpoint
- **Resiliency:** Backup and Restore, High Availability
- **Support:** Monitoring, Logging, and Support services

## Pre-certification questions
{: #pre-certification-scope}

Table 1 below captures the questions.
| Aspect | Question | Notes |
|---|---|---|
| General | Have you created a Contacts page so that after a deal closes everyone knows who was involved? | |
| | Is IBM responsible for defining the architecture and sizing? | |
| | Based on scope do you have Advise, Build Move and Manage organizations accounted for? Integrated RACI defined? | |
| | Are standard offerings used in the solution?  If not, are you using roadmap items? | |
| | Do you have Offering commitment in writing to delivery of roadmap item you are using in your solution? How far out is the roadmap item of the solution?  If over 30 days, did Offering team ask for Letter120? | |
| | When designing the timeline, have you considered lead times for things such as direct link, tooling,  and other dependencies? | |
| | Does the buildout have a ramp or is everything go in day 1? | |
| | Are DOUs in place for cross-LoB items (e.g IBM Cloud, IBM SW, Redhat SW)? | |
| | Have key Risk items been pulled from the RAID log and populated in the ISBD?  Have the risks been mitigated? | |
| Platform | Has the target environment been optimized taking into consideration the current application and infrastructure utilization? (Average, Peak etc.)? | |
| | Are we dependent on any POC or Benchmarks? | For what reason? |
| Storage | Is CIFS storage required? Endurance Storage does not support CIFS. |  |
| Networking | Are any transit gateways required? | |
| | What network is being used for DR replication and backups, and has bandwidth been calculated? (IBM backbone?  Direct Link egress? Megaport?) | |
| | How is the client connecting to the environment?  Direct Link?  VPN over internet? | |
| | Are any GRE or IPSEC tunnels required? | |
| | Is BYOIP a requirement and how have you solved for it? | |
| | Does the client have a good understanding of their responsibilities? i.e. - They need to extend their WAN to the PoP and cross connect to the Direct Link ports. | |
| | Have you solutioned Direct Link 1.0 or 2.0? DL 1.0 only connects to classic. DL 2.0 can connect to classic and VPC Gen2.  DL2.0 is metered.  Have you estimated those charges or captured proper contract language? | |
| | Are there multiple landing zones? Will those landing zones have different vlans. If the client's source workloads are all in one vlan, they will need to re-ip, if things are hardcoded.  | Ensure you understand vlan design. |
| Data | Have you solved for data encryption requirements? | at-rest and in transit |
| Security | Any key management requirements? | |
| Resiliency | Any SLAs around application or infrastructure availability? | |
| | What are the RTO/RPO? | likely will have tiers |
| | What are the requirements for scalability of the application or infrastructure? | |
| | Is DR required? | |
| | Is replication required? | Name tool to be used? |
| | What is the backup strategy? | |
| | What is the retention policy?| |
| Support | Has Advanced or Premium Support been included? \n  Which one and why? | |
| | Who owns overall Program Governance? | |
| | Who is doing the Low Level Design and Buildout?  If Client, do they have the skill to do so?  Do they need help from IBM? | GCAT, Cloud Expert Services, PES |
| | Who is providing Day 2 managed services? | Client, PES, TAOS, Kyndryl? |
| | Is IBM responsible for any third party? | |
| | Is e2e Service Management Defined? | |
| | Who has tooling responsibility? | |
{: caption="Table 1. Pre-certification question in each aspect" caption-side="bottom"}
