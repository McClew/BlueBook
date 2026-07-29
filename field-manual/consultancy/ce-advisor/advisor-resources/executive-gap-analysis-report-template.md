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
  actions:
    visible: true
---

# Executive Gap Analysis Report Template

{% hint style="info" %}
## Why this Format Works

1. <mark style="color:$primary;">**It's Non-Judgemental:**</mark> You are stating facts and solutions, not blaming the client for having bad security. (Hits the _Non-judgemental_ and _Professional Approach_ criteria).
2. <mark style="color:$primary;">**It's Collaborative:**</mark> You are offering a structured path forward ("We will schedule a brief maintenance window"). (Hits the _Collaborative approach_ criteria).
3. <mark style="color:$primary;">**It speaks their language:**</mark> Notice how the "Business Risk" section talks about _fraudulent invoices_ and _ransomware_, not _subnets_ or _CVSS scores_.
{% endhint %}

## \[Cover Page / Header]

Document: Cyber Essentials Gap Analysis & Remediation Plan

Client: \[Client Company Name]

Prepared By: \[Your Name/Consultancy]

Assured Service Provider Date: \[Date]

## 1. Executive Summary

_<mark style="color:$info;">The goal of this section is to give the business owner the bottom line in 60 seconds without using acronyms or jargon.</mark>_

"Following our assessment of \[Company Name]'s IT environment on \[Date], this report outlines your current readiness for Cyber Essentials certification.

Currently, the business \[is / is not] ready to pass the certification. We have identified \[Number] key areas that require attention before we can successfully submit your application. While some of these vulnerabilities expose the business to immediate risks—such as malware infections or unauthorized access to financial data—the good news is that they can be resolved using a phased approach designed to minimize disruption to your daily operations."

## 2. Assessment Scope

_<mark style="color:$info;">Briefly remind them what you looked at, which helps define boundaries.</mark>_

"This assessment covered all internet-facing IT infrastructure used for business purposes. This includes:

* The main office network boundary (e.g., the primary office router).
* Company-owned devices (laptops, desktops, mobile phones).
* Employee-owned devices used for work purposes (Bring Your Own Device / BYOD).
* Cloud services used to store company data (e.g., Google Workspace, Microsoft 365)."

## 3. Key Findings & Business Risk

_<mark style="color:$info;">List the major failures here. Do not just state the technical failure; map it to the business risk using the NCSC Small Business Guide principles.</mark>_

**Finding 1:** \[e.g., Unsupported Operating Systems]

* The Issue: We identified devices (e.g., \[Specific Device Name]) running \[e.g., Windows 8.1], which is an end-of-life operating system.
* The Business Risk: The manufacturer no longer provides security updates for this software. If a new cyber threat is discovered, these devices cannot be protected, leaving a permanently open door for hackers to access company files or deploy ransomware.
* CE Requirement: Security Update Management.

**Finding 2:** \[e.g., Lack of Multi-Factor Authentication (MFA)]

* The Issue: MFA is not currently enforced for all users accessing cloud services \[e.g., Google Workspace/Emails].
* The Business Risk: If an employee's password is stolen (e.g., via a phishing email), an attacker can easily log into your business accounts, read confidential emails, or send fraudulent invoices to your clients.
* CE Requirement: User Access Control.

_<mark style="color:$info;">(Repeat for other key findings like Shared Admin Accounts, Default Passwords on Routers, Lack of Software Firewalls, etc.)</mark>_

## 4. Phased Remediation Plan

_<mark style="color:$info;">This is where you show you understand their business operations by grouping the fixes using the matrix we built in Step 1.</mark>_

To achieve certification and secure the business while minimizing downtime, we recommend the following phased action plan:

**Phase 1:** Immediate Background Fixes (High Security Value, Zero Downtime) _We will implement these immediately. They will not disrupt staff workflows._

* \[Action 1: e.g., Change the default admin password on the office router.]
* \[Action 2: e.g., Remove administrative privileges from standard user accounts for daily tasks.]

**Phase 2:** Scheduled Security Updates (High Security Value, Minor Scheduled Disruption) _We will schedule a brief maintenance window (e.g., Friday at 4 PM) to implement these changes. Staff will receive a quick "How-To" guide prior to implementation._

* \[Action 1: e.g., Turn on Multi-Factor Authentication for all email accounts.]
* \[Action 2: e.g., Push outstanding software updates to all laptops and require a system reboot.]

**Phase 3:** Strategic Upgrades (Hardware/Software Replacement) _These require budget and planning. We will work with you to schedule these over the next \[X] weeks._

* \[Action 1: e.g., Purchase a replacement Windows 11 laptop for the device currently running Windows 8.1 and migrate the user's data.]

**Phase 4:** Final Compliance Checks (Low Disruption) _Final settings applied in the background before the official audit._

* \[Action 1: e.g., Configure all devices to block auto-run functionality for USB drives.]

## 5. Next Steps

"Once you have reviewed this report, we will schedule a 15-minute call to agree on the timelines for Phase 1 and Phase 2. Once all phases are complete, we will formally submit your application for Cyber Essentials certification."
