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

# SOC Infrastructure

## Core Technology Stack

The modern SOC infrastructure is built upon four primary categories of tools that work in tandem to detect and mitigate threats (Gartner, 2025).

* **SIEM (Security Information and Event Management):**\
  It collects, aggregates, and analyses log data from diverse environments. Leading platforms like FortiSIEM offer multi-tenant capabilities, allowing MSSPs to separate client data while using a single management pane.
* **SOAR (Security Orchestration, Automation, and Response):**\
  Critical for tackling the "lack of skilled staff" barrier. SOAR platforms automate repetitive tasks, such as initial alert enrichment and basic remediation, allowing analysts to focus on high-priority threats.
* **EDR/XDR (Endpoint/Extended Detection and Response):**\
  Provides deep visibility into endpoint activities (laptops, servers). XDR extends this by correlating data across endpoints, networks, and cloud environments.
* **NDR (Network Detection and Response):**\
  Monitors internal network traffic (East-West) to identify lateral movement that perimeter defences might miss.

***

## Infrastructure Architecture Models

MSSPs generally choose between three architectural approaches depending on customer requirements and data sensitivity:

| Model                      | Description                                                                                                                               | Use Case                                                                    |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| Centralised (Cloud-Based)  | All customer data is funnelled into a single, MSSP-hosted cloud SIEM.                                                                     | Small-to-medium businesses (SMBs) seeking cost-effective monitoring.        |
| Decentralised (On-Premise) | Collectors and SIEM instances reside within the customer's environment; only alerts are sent to the MSSP (Diva-portal, 2026).             | High-compliance industries (Finance, Gov) with strict data residency rules. |
| Hybrid SOC                 | Continuous monitoring is outsourced to the MSSP, but the customer retains an internal team for specialised incident response (ACM, 2023). | Large enterprises with existing but overwhelmed security teams.             |
