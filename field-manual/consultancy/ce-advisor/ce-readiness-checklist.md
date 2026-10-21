# CE Readiness Checklist

This is the single source of truth for checking whether an organisation meets Cyber Essentials, both before certification and in post-certification compliance reviews.

<mark style="color:$info;">**Standard:**</mark> NCSC _Cyber Essentials: Requirements for IT Infrastructure v3.3_ (April 2026)

<mark style="color:$info;">**Question set:**</mark> IASME **Danzell**. Applies to all assessment accounts created on or after **27 April 2026**. Accounts created earlier had six months to certify against v3.2 / Willow.

{% hint style="danger" %}
Items marked **🔴 AUTO-FAIL** fail the whole assessment on their own, regardless of every other answer.
{% endhint %}

{% hint style="info" %}
**How to use this page**

* Keep this page as the unticked master. Duplicate it (or export it) for each engagement.
* Every item must be true on the **date the certificate is issued** (the scheme's definition of "point in time") and maintained throughout the certification period.
* Record the evidence for every tick. "The client said so" is not evidence.
* Re-verify this page against the NCSC and IASME documents at each annual scheme update (normally April).
{% endhint %}

### Assessment Record

| Field                   | Value                                   |
| ----------------------- | --------------------------------------- |
| Organisation            |                                         |
| Legal entities in scope |                                         |
| Assessor / Advisor      |                                         |
| Assessment date         |                                         |
| Requirements version    | v3.3 (Danzell)                          |
| Assessment type         | Pre-CE / Post-CE review / CE+ readiness |
| Outcome                 |                                         |

***

## 0. Scope & Pre-Assessment

Scope is not a technical control, but every control check is meaningless if the scope is wrong. See [The Boundary & Scoping](the-boundary-and-scoping.md).

### Boundary

* [ ] Scope boundary is clearly defined: the **business unit** managing it, the **network boundary**, and the **physical location**.
* [ ] Scope has been agreed with the Certification Body before the assessment begins.
* [ ] Whole-organisation scope is used, **or** any sub-set is segregated from the rest of the organisation by a firewall or VLAN.
* [ ] Every exclusion is justified, with an explanation of how excluded networks are segregated from in-scope systems.
* [ ] Out-of-scope areas are described for the assessment (this is not published on the certificate).
* [ ] All legal entities in scope are listed with name, address and company number.
* [ ] Scope includes end user devices. A scope without end user devices is not acceptable.

### What Is In Scope

* [ ] All devices and software are captured that can accept inbound connections from the internet, can make outbound connections via the internet, or control data flow between those devices and the internet.
* [ ] Asset inventory is current: hardware, software (with versions and end-of-support dates), cloud services and accounts.

### Cloud Services

* [ ] All cloud services are identified, including shadow IT and SaaS signed up with a business email. A cloud service is any on-demand, scalable, shared-infrastructure, internet-accessible service accessed with organisational credentials or a business email that stores or processes organisational data.
* [ ] All cloud services are in scope. **Cloud services cannot be excluded.**
* [ ] Each service is classified as IaaS, PaaS or SaaS, and it is documented who implements each control (shared responsibility).
* [ ] Where the provider implements a control, its commitment is evidenced in a contract or in documents the contract references (security statement, trust centre).

### Devices & Users

* [ ] **BYOD:** user-owned devices that access organisational data or services are in scope. Devices used _only_ for native voice, native text or MFA apps are out of scope.
* [ ] **Home and remote working:** corporate and BYOD devices are in scope. Routers supplied by the organisation are in scope. ISP routers are out of scope, so a software firewall is required on the devices.
* [ ] **Corporate VPN:** if used, the internet boundary moves to the company firewall or virtual/cloud firewall, and the VPN is administered by the organisation.
* [ ] **Wireless devices:** in scope if they can communicate via the internet. Out of scope if they can only be attacked within signal range, or if they are part of a home ISP router.
* [ ] **Third-party and MSP accounts:** every account the organisation owns is in scope, even when it is used by a supplier, contractor or MSP. Controls on externally managed services can be evidenced.
* [ ] **Devices loaned to third parties:** devices the organisation owns and loans out are in scope. Devices owned by MSP administrators, contractors or customers are out of scope, as are student BYOD devices.
* [ ] **Web applications:** publicly available commercial web apps are in scope. Bespoke and custom components are out of scope (follow the Software Security Code of Practice).

***

## 1. Firewalls

<mark style="color:$info;">**Aim:**</mark> Only secure and necessary network services can be accessed from the internet.

<mark style="color:$info;">**Applies to:**</mark> boundary firewalls, desktops, laptops, routers, servers, IaaS, PaaS, SaaS.

* [ ] Every in-scope device is protected by a correctly configured firewall (a boundary firewall, or a network device with firewall functionality).
* [ ] A software firewall is enabled on every device used on networks the organisation does not control (home networks, public Wi-Fi). The built-in OS firewall is preferred.
* [ ] Default administrative passwords are changed to strong, unique passwords that meet the password rules in section 4, **or** remote administrative access is disabled entirely.
* [ ] The administrative interface is **not** reachable from the internet. Where it is, there is a clear, documented business need **and** it is protected by either MFA, or an IP allow list of a small range of trusted addresses combined with properly managed password authentication.
* [ ] Unauthenticated inbound connections are blocked by default.
* [ ] Every inbound rule is approved and documented by an authorised person, including the business need.
* [ ] Unnecessary rules are removed or disabled when no longer needed, and there is evidence of periodic rule review.
* [ ] For IaaS and PaaS, inbound access is restricted with data flow policies (security groups, NSGs, cloud firewalls).
* [ ] Firewall and router firmware is supported and patched (see section 3).

***

## 2. Secure Configuration

<mark style="color:$info;">**Aim:**</mark> Devices are configured to reduce vulnerabilities and provide only the services their role needs.

<mark style="color:$info;">**Applies to:**</mark> servers, desktops, laptops, tablets, mobile phones, thin clients, IaaS, PaaS, SaaS.

### Computers, Network Devices & Cloud Services

* [ ] Unnecessary user accounts are removed or disabled, such as guest accounts, unused admin accounts and vendor default accounts.
* [ ] Default or guessable account passwords are changed (see section 4).
* [ ] Unnecessary software is removed or disabled, including applications, system utilities and network services.
* [ ] Auto-run features that execute files without user authorisation are disabled (AutoRun/AutoPlay, auto-opening downloads).
* [ ] Users are authenticated before they can access organisational data or services.
* [ ] Configuration is managed proactively, with evidence of regular review and not just a one-off build.
* [ ] SaaS tenants are configured securely, for example sharing settings, unused apps and integrations, and legacy authentication.

### Device Unlocking

* [ ] A credential (biometric, password or PIN) is required before a physically present user can access a device's services.
* [ ] Unlock credentials are protected against brute force with either throttling (**no more than 10 guesses in 5 minutes**) or lockout after **no more than 10** failed attempts. Where neither can be configured, the vendor default is used.
* [ ] Credential quality is enforced by technical controls:
  * Unlock-only credential: minimum **6 characters** for the password or PIN.
  * Credential also used for authentication (for example a Windows password that is also the Entra ID or domain password): the full password rules in section 4 apply.

***

## 3. Security Update Management

<mark style="color:$info;">**Aim:**</mark> Devices and software are not vulnerable to known issues that have fixes available.

<mark style="color:$info;">**Applies to:**</mark> servers, desktops, laptops, tablets, mobile phones, firewalls, routers, IaaS, PaaS, SaaS.

{% hint style="info" %}
**"Software"** includes operating systems, commercial off-the-shelf applications, extensions, interpreters, scripts, libraries, network software, and firewall and router firmware.

**"Critical or high risk"** means any of: the vendor describes it as critical or high risk; it has a CVSS v3 base score of **7 or above**; or the vendor gives **no** severity details. If a bundled update fixes any critical or high issue, the whole update falls under the 14-day rule.
{% endhint %}

* [ ] All software in scope is **licensed and supported**: the organisation has a legal right to use it, and the vendor provides regular vulnerability fixes and has published a future end-of-support date.
* [ ] Unsupported software is removed from devices, **or** moved out of scope into a sub-set that prevents all traffic to and from the internet.
* [ ] All software is supported on the **date the certificate is issued**. Flag any end-of-support dates that fall within the certification year.
* [ ] Mobile and tablet OS versions still receive vendor security updates.
* [ ] Automatic updates are enabled wherever possible.
* [ ] 🔴 **AUTO-FAIL (A6.4):** all high-risk or critical security updates and vulnerability fixes for **operating systems and router/firewall firmware** are installed within **14 days** of release.
* [ ] 🔴 **AUTO-FAIL (A6.5):** all high-risk or critical security updates and vulnerability fixes for **applications, including associated files and extensions**, are installed within **14 days** of release.
* [ ] Patch compliance is verified across the **entire** scope, not just a sample (patch reports from RMM/MDM, vulnerability scans).
* [ ] Vulnerability fixes that are not traditional patches (registry fixes, configuration changes, vendor scripts) are tracked and applied within the same window.

{% hint style="success" %}
**Recommended, not mandatory:** apply **all** released updates within 14 days, whatever their severity.
{% endhint %}

***

## 4. User Access Control

<mark style="color:$info;">**Aim:**</mark> Accounts are assigned only to authorised individuals and give access only to what each role needs.

<mark style="color:$info;">**Applies to:**</mark> servers, desktops, laptops, tablets, mobile phones, IaaS, PaaS, SaaS. In every cloud model this control is **the organisation's responsibility**.

### Account Lifecycle

* [ ] There is a process to create and approve user accounts, with evidence such as tickets or approval records.
* [ ] Every user authenticates with unique credentials before accessing applications or devices. There are no shared accounts.
* [ ] Accounts are removed or disabled when no longer required, for leavers and after a defined period of inactivity.
* [ ] Special access privileges are removed when no longer required (movers and role changes).
* [ ] Third-party, supplier and MSP accounts are inventoried and controlled to the same standard.

### Multi-Factor Authentication

* [ ] 🔴 **AUTO-FAIL:** MFA is enabled on **every cloud service where it is available**, whether it is free, included or a paid option.
* [ ] MFA is implemented wherever else it is available, prioritising administrative accounts and accounts accessible from the internet.
* [ ] The password element of MFA is at least **8 characters** with **no maximum length**.
* [ ] Additional factors are one of: a managed or enterprise device, an app on a trusted device, a physically separate token, or a known or trusted account.
* [ ] Passwordless methods are recorded where used. Passkeys and FIDO2 authenticators count as MFA.

### Administrative Accounts

* [ ] Administrative activities are performed only with **separate** admin accounts.
* [ ] Admin accounts are not used for email, web browsing or other standard user activities. For example, they are not mail-enabled, and standard users have no local admin rights.
* [ ] An up-to-date list of who holds administrative privileges is maintained, including domain, local, cloud tenant and firewall admins.

### Password-Based Authentication

* [ ] Passwords are protected against brute force by at least one of: MFA; throttling (**no more than 10 guesses in 5 minutes**); or lockout after **no more than 10** failed attempts.
* [ ] Password quality is managed by technical controls, using one of:
  * MFA, **or**
  * minimum **12 characters**, no maximum length, **or**
  * minimum **8 characters**, no maximum length, **plus** automatic blocking of common passwords (deny list).
* [ ] Users are supported to choose unique passwords:
  * education on avoiding common passwords (pet names, keyboard patterns, reused passwords)
  * longer passwords encouraged, such as three random words
  * usable secure storage provided (a password manager or locked cabinet), with clear guidance on its use
  * **no** enforced regular password expiry
  * **no** enforced complexity requirements
* [ ] There is an established process to change passwords promptly when compromise is known or suspected.

***

## 5. Malware Protection

<mark style="color:$info;">**Aim:**</mark> Execution of known malware and untrusted software is restricted.

<mark style="color:$info;">**Applies to:**</mark> servers, desktops, laptops, tablets, mobile phones, IaaS, PaaS, SaaS.

* [ ] **Every** in-scope device has at least one of the two mechanisms below, and it is **active**, kept up to date per vendor instructions, and configured as described.

### Option A: Anti-Malware Software (Windows & macOS devices, including servers)

* [ ] Updated in line with vendor recommendations.
* [ ] Prevents malware from running.
* [ ] Prevents execution of malicious code.
* [ ] Prevents connections to malicious websites over the internet (web protection or web filtering is enabled).

### Option B: Application Allow Listing (any in-scope device)

* [ ] Only approved applications, restricted by code signing, can execute.
* [ ] Applications are actively approved before being deployed to devices.
* [ ] A current list of approved applications is maintained.
* [ ] Users cannot install any application that is unsigned or has an invalid signature.

### Coverage Checks

* [ ] Mobile devices (iOS/Android) meet Option B: installs restricted to official stores or MDM-approved apps, with sideloading blocked.
* [ ] Linux and other non-Windows/macOS devices have a documented mechanism. Option A is listed only for Windows and macOS.
* [ ] For SaaS and PaaS, the provider's malware protection commitment is documented (see Cloud Services in section 0).

***

## 6. Declaration & Ongoing Compliance

* [ ] The verified self-assessment (VSA) declaration is signed by a board member or director. It acknowledges responsibility for maintaining compliance with all controls **throughout the certification period**.
* [ ] A post-certification review cadence is agreed. Re-run this checklist periodically, with particular attention to new cloud services, leavers, MFA coverage, 14-day patch compliance, firewall rule changes and upcoming end-of-support dates.

***

## 7. Cyber Essentials Plus Readiness

Only applies if the organisation is going on to CE+. See [CE+ Technical Audit](ce+-technical-audit.md).

* [ ] The VSA is completed and **finalised before CE+ testing begins**. Answers **cannot be changed** in response to CE+ results.
* [ ] Updates are applied across the **whole** CE+ scope, not only the devices likely to be sampled.
* [ ] The client understands the retest rule. If the initial sample fails on updates, the retest re-checks the original sample **and** a **new random sample**. A **second failure revokes** the Cyber Essentials (VSA) certificate.

***

## Recommended (Not Assessed)

* [ ] **Backups:** not a technical requirement, but strongly recommended. Back up regularly and automatically where possible. Disconnect USB or external backup drives when a backup isn't running.
* [ ] **MFA strength:** SMS is acceptable but the weakest option. Prefer authenticator apps, passkeys or FIDO2 keys where they work for the organisation.
* [ ] **Asset management:** not a CE control, but it underpins all five. Maintain authoritative, actively used asset data rather than a list nobody updates.

***

## Sources

* [NCSC: Cyber Essentials Requirements for IT Infrastructure v3.3 (PDF)](https://www.ncsc.gov.uk/files/cyber-essentials-requirements-for-it-infrastructure-v3-3.pdf)
* [IASME: Changes to Cyber Essentials for April 2026](https://iasme.co.uk/articles/important-update-changes-to-cyber-essentials-for-april-2026/)
* [IASME: Preview the self-assessment questions (Danzell)](https://iasme.co.uk/cyber-essentials/preview-the-self-assessment-questions-for-cyber-essentials/)
