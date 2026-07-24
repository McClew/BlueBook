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

# CE+ Technical Audit

For CE+ a Cyber Advisors role shifts from simply _implementing_ the controls to _proving_ they work under audit conditions.

***

## CE vs. CE+

The most important concept to grasp - and explain to clients - is that the technical requirements for CE and CE+ are exactly the same. There are no "extra" hidden controls in CE+.

The difference lies entirely in _how compliance is verified_.

* **Cyber Essentials (Basic):** A verified self-assessment. The client answers a questionnaire on the IASME portal, declaring that they meet the controls. An external assessor reviews the answers for logical consistency, but does not physically check the network. It relies on trust and honesty.
* **Cyber Essentials Plus (CE+):** A hands-on technical audit. An independent Certification Body assessor physically (or remotely) accesses the client's network and workstations to scientifically test that the claims made in the CE questionnaire are true.

{% hint style="info" %}
#### The 3-Month Window

A company must pass the basic CE self-assessment before they can undertake CE+. The CE+ audit must be completed within 3 months of their basic CE certification date.
{% endhint %}

***

## CE+ Processes & Testing Specification

During a CE+ audit, the assessor will not test every single device in the company. Instead, they test a representative Sample Set of devices across different operating systems, builds, and locations (including remote workers and BYOD).

According to the _CE+ Test Specification_, the auditor will perform specific technical tests, primarily focusing on the following areas:

* **Vulnerability Scanning (Patching):** The assessor will run an authenticated (credentialed) vulnerability scan against the sample devices using tools like Nessus or Qualys. If the scan finds any "High" or "Critical" vulnerabilities (CVSS 7.0 or above) that have been missing a patch for more than 14 days, it is an automatic failure.
* **Malware Protection Testing:** The assessor will attempt to execute malicious code. They typically do this by emailing safe test files (like the EICAR test string) and attempting to download them via the web browser to see if the system's anti-malware actively blocks or quarantines the file upon access.
* **Account Separation:** The assessor will check the logged-in user on the sampled machines to verify they are not running as a Local Administrator for everyday tasks.
* **MFA Verification:** The assessor will ask users to log into cloud services (like Microsoft 365) to physically witness the MFA prompt occurring.

***

## Preparing the Client for the Audit

This is where an Assured Service Provider provides massive value. Failing a CE+ audit means the client has 30 days to fix the issue and often has to pay for a re-test.

### CE+ Prep Playbook

1. **Conduct Pre-Audit Vulnerability Scans:** Do not trust the IT provider's patch management dashboard. Run your own credentialed vulnerability scans on a sample of devices (especially remote laptops and BYOD). Find the missing patches before the auditor's Nessus scanner does.
2. **Run the EICAR Tests:** Manually send the EICAR test file via email to the client's inboxes and attempt to open it. Verify that their endpoint protection triggers an alert and blocks the file.
3. **Audit Cloud Access Logs:** Do not just ask "Is MFA on?" Check the Azure AD or Google Workspace sign-in logs. Look for legacy authentication protocols that might be bypassing MFA.
4. **Evidence Gathering:** Help the client collect screenshot evidence of Mobile Device Management (MDM) configurations, firewall rules, and password policies to speed up the auditor's workflow.
