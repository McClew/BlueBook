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

# The Five Technical Controls

{% hint style="info" %}
_Up-to-date for CE v3.3._
{% endhint %}

Cyber Essentials mitigates 80% if the most common internet-borne cyber attacks by mandating strict compliance across five technical control themes. Every in-scope device and service must meet the requirements for all applicable controls.

***

## Firewalls & Internet Gateways

**Objective:** To create a secure buffer between the organisations infrastructure and other,. untrusted networks.

**Requirements:**

* **Firewalls:** Every device that is in scope must be protected by a firewall. This can be a boundary firewall, a host-based software firewall, or both.
* **Change Default Passwords:** The default administrative password for any firewall or router must be changed to an alternative that is at **least 8 characters long** and cannot be easily guessed.
* **Block Unauthenticated Connections:** Unauthenticated inbound network connections must be blocked by default.
* **Documented Rules:** Any open inbound network ports must have a documented business case and be approved by an authorised person.
* **Remove Unused Rules:** Firewall rules must be reviewed on a regular basis, and ports must be closed when they are no longer required.

***

## Secure Configuration

**Objective:** To reduce the inherent vulnerabilities in computers and software by stripping away unnecessary features and changing insecure default settings.

**Requirements:**

* **Disable Unused Accounts:** All unnecessary user accounts, such as guest accounts or accounts for former employees, must be removed or disabled.
* **Remove Unnecessary Software:** All unnecessary software, applications, and network services must be removed or disabled to reduce the attack surface.
* **Change Default Credentials:** Default passwords for all software and devices must be changed to unique, strong passwords.
* **Disable Auto-run:** Auto-run and auto-play features - which automatically execute code from USB drives or downloaded files - must be disabled.
* **Device Authentication:** Devices must require authentication via a password, PIN, or biometric check to unlock.
* **Device Locking:** Devices must be configured to automatically lock after a maximum of 15 minutes of inactivity.

***

## User Access Control

**Objectives:** To ensure only authorised individuals have access to data and service, and that they only have the minimum level of access required to fulfil the tasks required of their role.

**Requirements:**

* **Unique Accounts:** Every user must have their own unique, named account. Shared accounts must not be used for everyday tasks.
* **Principle of Least Privilege:** Users must only be provided with the minimum privileges required to perform their specific role.
* **Administrative Accounts:** Administrative accounts must only be used for administrative tasks. Administrators must use a separate standard account for daily tasks.
* **Multi-Factor Authentication:** MFA is mandatory for all administrative accounts, **AND** for all users accessing any cloud services.
* **Password Policies:** Passwords must meet one of the following three complexity standards:
  * Minimum 8 characters **AND** MFA
  * Minimum 8 characters **AND** anti-brute-force technical controls, such as:
    * Account lockout after 10 failed attempts **OR**;
    * Throttling the guesses to no more than 10 within a 5-minute period.
  * Minimum 12 characters (if neither of the above are possible).
* **Leavers Policy:** Organisations must have a _documented process_ to promptly remove or disable user access when an employee leaves or no longer requires access.

{% hint style="warning" %}
#### Password Policy Nit-picking

IASME may require confirmation that "No maximum password length" has been set on the password policies.
{% endhint %}

***

## Malware Protection

**Objective:** To restrict the execution of known malware and untrusted software to prevent harm to systems.

**Requirements:**

For all in-scope devices, the organisation must implement at least one of the following three mechanisms:

* **Anti-Malware Software:**
  * Must be active and kept up to date.
  * Must update its signature files at least daily.
  * Must be configured to scan files automatically upon access (e.g., when opening, executing, or downloading a file).
  * Must prevent malicious code from executing.
* **Application Allow-listing:**
  * Only explicitly approved applications are permitted to execute on the device.
  * All other unapproved applications are blocked by default.
  * Users must not be able to install any application that is unsigned or has an invalid signature.
* **Application Sandboxing** (natively built-in and acceptable by default for mobile OSs)**:**
  * All application code is forced to run within an isolated environment.
  * The sandbox prevents the application from interacting with other applications, data, or core operating system functions without explicit user permission.

***

## Security Update Management

**Objective:** To ensure that all software and operating systems are kept up to date so that known vulnerabilities are patched before attackers can exploit them.

**Requirements:**

* **Supported Software:** All operating systems, applications, and firmware must be licensed and supported by the vendor (they still receive security updates). If it is unsupported, it is an automatic failure.
* **Unsupported Software:** Unsupported software must be entirely removed from in-scope devices.
* **The 14-Day Rule:** All security updates labelled by the vendor as "High" or "Critical" severity (or with a CVSS v3 score of 7.0 and above) must be applied within 14 days of release.
* **Auto-Updates:** Where possible, automatic updates should be enabled to ensure compliance and assist in meeting the 14-day requirement.
