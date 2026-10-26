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
  anchors:
    visible: true
---

# Mobile Device Management

## BYOD: Bring Your Own Device

BYOD is the term for when organisational IT infrastructures have to deal with computing and communications equipment, software, security tools, and data that do not belong to the organisation and are not under its legal span of control.

Vendors, customers, prospective employees and visitors of any kind to the business's locations - even family and friends of employees - can bring in their own phones, laptops, tablets and smart devices all with varying expectations about connecting to or making use of the organisation's IT infrastructure.

In many cases it is to the company's advantage to encourage employees to own and operate their own equipment, but it comes with up-front and downstream costs and risks.

#### <mark style="color:red;">Concerns</mark>

* <mark style="color:red;">**Data Leakage and Loss:**</mark> Corporate data can easily blend with personal data. This results in unintended syncing to personal cloud backups, accidental sharing via personal apps, or data remaining accessible after an employee leaves the company.
* <mark style="color:red;">**Malware Cross-Contamination:**</mark> Personal endpoints are highly susceptible to malicious apps downloaded from unofficial stores, mobile phishing (smishing), and spyware. Once a compromised device connects to the internal network, it can act as a bridge for lateral movement.&#x20;
* <mark style="color:red;">**Unpatched Operating Systems:**</mark> Unlike corporate hardware, IT teams cannot force critical security updates on user-owned assets. Outdated software leaves known vulnerabilities exposed indefinitely.
* <mark style="color:red;">**Unsecured Network Connections:**</mark> Employees frequently connect to unencrypted public Wi-Fi hotspots, opening the door to man-in-the-middle attacks and interception of data in transit.
* <mark style="color:red;">**Privacy and Legal Gaps:**</mark> Enforcing strict oversight can accidentally expose an employee's personal photos, location history, or web browsing. This creates balancing hurdles between data compliance (like GDPR or HIPAA) and personal user privacy.

#### <mark style="color:$primary;">Security Controls</mark>

To securely manage BYOD, technical architectures should transition away from full-device control and instead focus on a modern **Zero Trust approach** that wraps security directly around identities, data, and applications.

<table><thead><tr><th>Control Category</th><th width="389">Specific Technical Implementations</th><th>Purpose</th></tr></thead><tbody><tr><td><strong>Application &#x26; Data Isolation</strong></td><td><mark style="color:$primary;"><strong>Containerisation (MAM / Work Profiles)</strong></mark><br>• Creates a cryptographically isolated work profile on the personal phone.<br>• Separates corporate storage from personal apps.<br>• Enforces <strong>Selective Wipe</strong> (removes corporate profile without deleting personal photos/apps).</td><td>Prevents data leakage into personal apps or local cloud storage.</td></tr><tr><td><strong>Identity &#x26; Access Management</strong></td><td><mark style="color:$primary;"><strong>Conditional Access</strong></mark><br>• Grants network entry based on real-time risk context.<br>• Mandatory Multi-Factor Authentication (MFA).<br>• Device posture checks (denies entry if the phone is jailbroken/rooted).</td><td>Restricts access if the endpoint fails basic security baseline tests.</td></tr><tr><td><strong>Network &#x26; Transit Protection</strong></td><td><mark style="color:$primary;"><strong>Micro-segmentation &#x26; Zero Trust Network Access (ZTNA)</strong></mark><br>• Replaces broad-network legacy VPNs with application-specific tunnels.<br>• Isolates untrusted endpoints within segmented VLANs.</td><td>Minimises lateral movement across internal servers if a personal device is compromised.</td></tr><tr><td><strong>Threat &#x26; Endpoint Defense</strong></td><td><mark style="color:$primary;"><strong>Mobile Threat Defense (MTD)</strong></mark><br>• Continuously scans for malicious network patterns, smishing links, and embedded malware.<br>• Enforces minimum OS update requirements (e.g., must patch within 14 days).</td><td>Actively detects ongoing mobile threats without peering into personal usage logs.</td></tr><tr><td><strong>Governance &#x26; Operations</strong></td><td><mark style="color:$primary;"><strong>Comprehensive BYOD Policy &#x26; Logging</strong></mark><br>• Clear procedural terms on acceptable use and instant loss-reporting.<br>• Log collection of enterprise data events to support incident response workflows.</td><td>Ensures clear alignment on security responsibilities and maintains a clean regulatory audit trail.</td></tr></tbody></table>

***

## COPE & CYOD

<mark style="color:$info;">Company-owned personally enabled (COPE)</mark> refers to strategies in which the organisation owns and exerts some configuration management, application allowed/blocked list management, and security feature enforcements on the device it issued to an individual employee.

The employee can then, within policy limits, install applications and data for work-related or purely personal use. An example described in this context is a university that provides laptops to its full-time faculty for work-related teaching, courseware development, research and organisational service tasks, knowing that the laptops can and will be used for purely personal activities as well.

<mark style="color:$info;">Choosing your own device (CYOD)</mark> is a common variation on the COPE theme, in which the organisation owns or leases a smaller set of device types and issues them to employees to use with company systems and data.

Employees can choose from this limited set but are restricted from using personally owned devices with company data or systems.

While this reduces IT configuration management issues and makes the threat surface more manageable, it does not directly address visitor, customer, client or guest use of mobile devices at the edges of the organisations systems.

Both COPE and CYOD can refer to company or corporate ownership or lease and management of the devices.
