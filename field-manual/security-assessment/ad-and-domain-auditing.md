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

# AD & Domain Auditing

An Active Directory (AD) & Domain Audit is a comprehensive evaluation of a Windows Domain environment's security posture. It focuses on the configurations, permissions, and structural relationships within the directory services that manage an organisation’s identities and resources.

***

## The Goal

The primary objective is to identify and mitigate risks that could lead to full domain compromise. Key goals include:

* **Privilege Discovery:** Mapping who has administrative rights and why.
* **Configuration Review:** Identifying weak protocols (e.g., LLMNR/NBT-NS) or insecure settings.
* **Hygiene Assessment:** Spotting stale accounts, weak passwords, and dormant elevated sessions.
* **Compliance:** Ensuring the environment aligns with security frameworks like Cyber Essentials Plus or ISO 27001.

***

## Utilising BloodHound CE for Audits

BloodHound CE is the industry-standard tool for visualising the "hidden" relationships within AD. During an audit, we use it to:

1. **Collect Data:** Utilise `SharpHound` or `AzureHound` to ingest object properties, group memberships, and active sessions.
2. **Graph Analysis:** Instead of looking at isolated users, BloodHound allows us to see how a low-privileged account might have `GenericAll` rights over a group that, in turn, has local admin rights on a Domain Controller.
3. **Identify Tier 0 Exposure:** We run specific Cypher queries to find every possible path from a standard "Domain User" to "Domain Admin" privileges.

***

## Audit Deliverables

At the conclusion of an AD Audit, the client should receive:

* **Executive Summary:** A high-level risk score and a "State of the Domain" overview.
* **The Attack Path Map:** Visual evidence of the most dangerous routes to Domain Admin.
* **Remediation Roadmap:** A prioritised list of "Quick Wins" (e.g., removing a specific nested group) and long-term architectural changes (e.g., implementing Tiered Administration).
* **Technical Appendices:** Lists of inactive accounts, Kerberoastable users, and misconfigured Group Policy Objects (GPOs).
