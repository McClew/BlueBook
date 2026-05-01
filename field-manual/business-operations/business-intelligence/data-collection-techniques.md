---
layout:
  width: default
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
  metadata:
    visible: true
  tags:
    visible: true
---

# Data Collection Techniques

To drive [data-driven-sales.md](data-driven-sales.md "mention"), the technical stack must be viewed as a sensor array for business opportunities. This article outlines the specific telemetry points available within common MSP/MSSP toolsets and how to extract them to build a quantitative business case for the client.

{% hint style="success" icon="handshake" %}
### The "Proactive Partnership" Mindset

When collecting this data, the goal is not to "find a problem to sell a fix." The goal is to curate a story of the client’s environment.


{% endhint %}

{% hint style="warning" %}
## Automated reporting is a baseline; Curated Insights are a premium.

Don't just send the raw RMM reports - extract the data and say:

_"We noticed 15% of your infrastructure will hit End-of-Life in Q3; let's budget for that now so you don't take a productivity hit later."_
{% endhint %}

***

## RMM: Hardware & Lifecycle Telemetry

RMM platforms are the primary source for Infrastructure Sales. It provides the "Health Baseline" of the client's environment.

<table><thead><tr><th width="221">Data Point</th><th width="237">Collection Method</th><th>Sales Pivot</th></tr></thead><tbody><tr><td>Battery/Disk Health</td><td>SMART status scripts / API exports.</td><td>Proactive hardware refresh before failure-induced downtime.</td></tr><tr><td>OS/Software EoL</td><td>Registry crawls / Version auditing.</td><td>Projects for OS upgrades or "Software-as-a-Service" migrations.</td></tr><tr><td>Asset Sprawl</td><td>Network discovery scans.</td><td>Charging per-node; uncovering "shadow" devices that aren't under contract.</td></tr><tr><td>Performance Bottlenecks</td><td>CPU/RAM historical logging.</td><td>Upselling higher-spec hardware for "Power Users" (Engineers/Designers).</td></tr></tbody></table>

***

## EDR/MDR: Hygiene & Exposure Telemetry

EDR (Endpoint Detection and Response) and MDR platforms act as sensors for Security Maturity Sales.

* **Vulnerability Surface:** Extracting "Top 10 Missing Patches" or "Unpatched CVEs." This proves the need for an automated patch management add-on.
* **Local Admin Proliferation:** Scripting a check for users with local admin rights. This data is the "smoking gun" needed to sell PAM (Privileged Access Management) solutions.
* **Rogue Device Discovery:** MDR logs often show "unmanaged" devices communicating on the network. This supports a pitch for NAC (Network Access Control) or a clean-up project.
* **Near-Miss Analytics:** Tracking the number of blocked "Pre-Execution" threats. This visualises the "Invisible Value" of the MSSP, justifying contract renewals.

***

## Firewall & Gateway: Connectivity Telemetry

Firewalls provide the data for Network Architecture & Policy Sales.

* **Bandwidth Saturation:** Identifying when the circuit hits 90% capacity during business hours. This provides objective evidence for a Bandwidth Upgrade or SD-WAN implementation.
* **Geo-IP Activity:** Collecting logs of traffic hitting the firewall from "High Risk" countries where the client doesn't do business. This drives sales for Geo-Fencing and Identity Protection (MFA).
* **Shadow IT/SaaS Usage:** Analysing outgoing web traffic to identify unauthorised cloud apps (e.g., users using personal Dropbox vs. corporate OneDrive). This leads to CASB (Cloud Access Security Broker) or "Cloud Governance" projects.

### Search History Data Collection

