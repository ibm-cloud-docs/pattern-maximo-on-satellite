---

copyright:
  years: 2024
lastupdated: "2024-02-15"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

---

{{site.data.keyword.attribute-definition-list}}

# Network design
{: #network-design}

Networking is a key aspect of any cloud deployment but specifically for this pattern of deploying Maximo® Application Suite (MAS) on IBM Cloud Satellite in an on-premises Satellite location. There are many requirements to consider like security, resiliency, latency, throughput, etc., but the two critical ones from a {{site.data.keyword.satelliteshort}} perspective are bandwidth connectivity and certain reserved IPs. And from a MAS perspecitve establishing direct link (DL), or VPN connectivity is key.

\n  Listed below are some of the key requirements from a network perspective:

- Hosts must have minimum network bandwidth connectivity of 100 Mbps, with 1 Gbps preferred.
- Host IP addresses must remain static and cannot change over time.
- All {{site.data.keyword.satelliteshort}} hosts must have an IPv4 address since {{site.data.keyword.satelliteshort}} does not support IPv6. For more information, see [Host network requirements](/docs/satellite?topic=satellite-reqs-host-network).


The table shows IP address ranges that are reserved for {{site.data.keyword.satellitelong_notm}} and should not be used for any other purpose.
| Location type | IP range |
|---|---|
| Non-CoreOS enabled locations | 172.16.0.0/16, 172.18.0.0/16, 172.19.0.0/16, 172.20.0.0/16, and 192.168.255.0/24 |
| CoreOS enabled locations | 172.20.0.0/16 and 172.16.0.0/16 |
{: caption="Table 1. Reserved IP Addresses" caption-side="bottom"}

\n  Finally, the system clocks on the {{site.data.keyword.satelliteshort}} hosts at the on-premises location should be synced.
