---

copyright:
  years: 2024
lastupdated: "2025-06-17"

subcollection: pattern-maximo-on-satellite

keywords: Satellite, location, Maximo, MAS

---

{{site.data.keyword.attribute-definition-list}}

# Network design
{: #network-design}

Networking is a key aspect of any cloud deployment. Consider the following network design information for deploying {{site.data.keyword.prodname_imas_full_notm}} on {{site.data.keyword.satellitelong_notm}} in an on-premises Satellite location. There are many requirements to consider like security, resiliency, latency, throughput, but the two critical ones from a {{site.data.keyword.satelliteshort}} perspective are bandwidth connectivity and certain reserved IPs. From a MAS perspective, performance is key.

Review the following key requirements from a network perspective:

- For {{site.data.keyword.prodname_imas_short}}, network and storage should work together ensuring a disk throughput > 200 MB/s with a storage class delivering 100+ IOPS.
- Establish connectivity with either Direct Link (DL) or VPN connectivity.
- Satellite Hosts must have a minimum network bandwidth connectivity of 100 Mbps, with 1 Gbps preferred.
- Satellite Host IP addresses must remain static and cannot change over time.
- All {{site.data.keyword.satelliteshort}} hosts must have an IPv4 address since {{site.data.keyword.satelliteshort}} does not support IPv6.

For more information, see [Host network requirements](/docs/satellite?topic=satellite-reqs-host-network).


Review the following IP address ranges that are reserved for {{site.data.keyword.satellitelong_notm}} and should not be used for any other purpose.

| Location type | IP range |
|---|---|
| Non-CoreOS enabled locations | 172.16.0.0/16, 172.18.0.0/16, 172.19.0.0/16, 172.20.0.0/16, and 192.168.255.0/24 |
| CoreOS enabled locations | 172.20.0.0/16 and 172.16.0.0/16 |
{: caption="Reserved IP Addresses" caption-side="bottom"}

The system clocks on the {{site.data.keyword.satelliteshort}} hosts at the on-premises location should be synced.
{: note}
