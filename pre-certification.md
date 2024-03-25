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
- **Application:** All applications + licenses
- **Platform:** Classic, VPC, VMware
- **Storage:** Primary Storage, Backup Storage
- **Networking:** Enterprise Connectivity, Network Segmentation
- **Data:** Data Storage and data security
- **Security:** Identity and Access Management, Infrastructure and Endpoint
- **Resiliency:** Backup and Restore, High Availability
- **Support:** Monitoring, Logging, and Support services

## Pre-certification questions
{: #pre-certification-scope}

The table below captures the high-level questions.
| Category | Question | Notes |
|---|---|---|
| General | Have you created a Contacts page so that after a deal closes everyone knows who was involved? | |
| | *Who is responsible for defining the architecture and sizing?* | *Client/IBM* |
| | Based on scope do you have Advise, Build Move and Manage organizations accounted for? Integrated RACI defined? | |
| | Are standard offerings used in the solution?  If not, are you using roadmap items? | |
| | Do you have Offering commitment in writing to delivery of roadmap item you are using in your solution? How far out is the roadmap item of the solution?  If over 30 days, did Offering team ask for Letter120? | GA/Roadmap |
| | When designing the timeline, have you considered lead times for things such as direct link, tooling, and other dependencies? | |
| | Does the buildout have a ramp or is everything go in day 1? | |
| | Have key risk items been pulled from the RAID log for the proposed solution? | |
| | Describe how the risks have been mitigated | |
| | | |
| *Legal* | *Are DOUs in place for cross-LoB items or 3rd party providers (e.g IBM Cloud, IBM SW, Redhat SW)?* | |
| | *Are any SLAs defined for application or infrastructure availability? Explain how these will be measured and what penalties will apply.* | |
| | | |
| Application | What licenced software is used? List them. | |
| | Who owns the licences? | - IBM  \n - Client  \n - 3rd party |
| | Are there any application latency requirements that must be met? | Yes/NA |
| | Describe how the designed solution meets application latency requirements | |
| | | |
| Platform | Has the target environment been optimized taking into consideration the current application and infrastructure utilization? (Average, Peak etc.)? | |
| | Are we dependent on any POC or Benchmarks? | For what reason? |
| | | |
| Storage | What storage types have been included in the solution? | Block tiers/file/object/vSAN/Other |
| | Describe which tiers were needed for which data types or tiers | Prod / Dev / QA / Archive |
| | Is CIFS storage required? Endurance Storage does not support CIFS. | |
| | Has storage growth been accounted for? Describe the growth rates over time | |
| | | |
| Networking | Are any transit gateways required? | |
| | What network is being used for DR replication and backups, and has bandwidth been calculated? (IBM backbone?  Direct Link egress? Megaport?) | |
| | How is the client connecting to the environment? | - Direct Link /  DL Dedicated / VPN over internet |
| | *Are any GRE or IPSEC tunnels required?* | |
| | Is BYOIP a requirement in classic deal? | Yes / No |
| | If BYOIP is required, how have you solved for it? | |
| | *Does the client have a good understanding of their responsibilities? i.e. - They need to extend their WAN to the PoP and cross connect to the Direct Link ports.* | |
| | *Have you solutioned Direct Link 1.0 or 2.0? DL 1.0 only connects to classic. DL 2.0 can connect to classic and VPC Gen2.  DL2.0 is metered.  Have you estimated those charges or captured proper contract language?* | |
| | Are there multiple landing zones? Will those landing zones have different vlans. If the client's source workloads are all in one vlan, they will need to re-ip, if things are hardcoded.  | Ensure you understand vlan design. |
| | | |
| Data | Have you solved for data encryption requirements? | at-rest / in transit |
| | | |
| Security | Any key management requirements? | Yes / No |
| | What type of security services are required? Describe how these requirements are being met. | IAM / IDS / IPS / SIEM / DDoS / Other |
| | | |
| Resiliency | Any SLAs around application or infrastructure availability? | |
| | What are the requirements for scalability of the application or infrastructure? | |
| | Is DR required? If so, what are the RTO/RPO requirements? | NA / Hot / Warm/ Cold |
| | Is replication required? | Name tool to be used? |
| | What is the backup strategy? | Backup schedule / Retention policy |
| | | |
| Support | Has Advanced or Premium Support been included? Which one and why? |  Advanced / Premium |
| | Who owns overall Program Governance? | Cliet / IBM / 3rd Party |
| | Who is doing the Low Level Design and Buildout? | Client / TEL / BP / Other |
| | Who is providing Day 2 managed services? | Client / PES / TAOS / Kyndryl |
| | Is IBM responsible for any third party? | |
| | Is e2e Service Management Defined? | |
| | Who has tooling responsibility? | |
{: caption="Table 1. Pre-certification question in each category" caption-side="bottom"}
