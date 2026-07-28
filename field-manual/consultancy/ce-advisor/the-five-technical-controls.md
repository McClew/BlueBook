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

<mark style="color:$info;">**Objective:**</mark> To create a secure buffer between the organisations infrastructure and other, untrusted networks.

#### Requirements:

* <mark style="color:$warning;">**Firewalls:**</mark> Every device that is in scope must be protected by a firewall. This can be a boundary firewall, a host-based software firewall, or both.
* <mark style="color:$warning;">**Change Default Passwords:**</mark> The default administrative password for any firewall or router must be changed to an alternative that is at **least 8 characters long** and cannot be easily guessed.
* <mark style="color:$warning;">**Block Unauthenticated Connections:**</mark> Unauthenticated inbound network connections must be blocked by default.
* <mark style="color:$warning;">**Documented Rules:**</mark> Any open inbound network ports must have a documented business case and be approved by an authorised person.
* <mark style="color:$warning;">**Remove Unused Rules:**</mark> Firewall rules must be reviewed on a regular basis, and ports must be closed when they are no longer required.

***

## Secure Configuration

<mark style="color:$info;">**Objective:**</mark> To reduce the inherent vulnerabilities in computers and software by stripping away unnecessary features and changing insecure default settings.

#### Requirements:

* <mark style="color:$warning;">**Disable Unused Accounts:**</mark> All unnecessary user accounts, such as guest accounts or accounts for former employees, must be removed or disabled.
* <mark style="color:$warning;">**Remove Unnecessary Software:**</mark> All unnecessary software, applications, and network services must be removed or disabled to reduce the attack surface.
* <mark style="color:$warning;">**Change Default Credentials:**</mark> Default passwords for all software and devices must be changed to unique, strong passwords.
* <mark style="color:$warning;">**Disable Auto-run:**</mark> Auto-run and auto-play features - which automatically execute code from USB drives or downloaded files - must be disabled.
* <mark style="color:$warning;">**Device Authentication:**</mark> Devices must require authentication via a password, PIN, or biometric check to unlock.
* <mark style="color:$warning;">**Device Locking:**</mark> Devices must be configured to automatically lock after a maximum of 15 minutes of inactivity.

***

## User Access Control

<mark style="color:$info;">**Objectives:**</mark> To ensure only authorised individuals have access to data and service, and that they only have the minimum level of access required to fulfil the tasks required of their role.

#### Requirements:

* <mark style="color:$warning;">**Unique Accounts:**</mark> Every user must have their own unique, named account. Shared accounts must not be used for everyday tasks.
* <mark style="color:$warning;">**Principle of Least Privilege:**</mark> Users must only be provided with the minimum privileges required to perform their specific role.
* <mark style="color:$warning;">**Administrative Accounts:**</mark> Administrative accounts must only be used for administrative tasks. Administrators must use a separate standard account for daily tasks.
* <mark style="color:$warning;">**Multi-Factor Authentication:**</mark> MFA is mandatory for all administrative accounts, **AND** for all users accessing any cloud services.
* <mark style="color:$warning;">**Password Policies:**</mark> Passwords must meet one of the following three complexity standards:
  * Minimum 8 characters **AND** MFA
  * Minimum 8 characters **AND** anti-brute-force technical controls, such as:
    * Account lockout after 10 failed attempts **OR**;
    * Throttling the guesses to no more than 10 within a 5-minute period.
  * Minimum 12 characters (if neither of the above are possible).
* <mark style="color:$warning;">**Leavers Policy:**</mark> Organisations must have a _documented process_ to promptly remove or disable user access when an employee leaves or no longer requires access.

{% hint style="warning" %}
#### Password Policy Nit-picking

IASME may require confirmation that "No maximum password length" has been set on the password policies.
{% endhint %}

***

## Malware Protection

<mark style="color:$info;">**Objective:**</mark> To restrict the execution of known malware and untrusted software to prevent harm to systems.

#### Requirements:

For all in-scope devices, the organisation must implement at least one of the following three mechanisms:

* <mark style="color:$warning;">**Anti-Malware Software:**</mark>
  * Must be active and kept up to date.
  * Must update its signature files at least daily.
  * Must be configured to scan files automatically upon access (e.g., when opening, executing, or downloading a file).
  * Must prevent malicious code from executing.
* <mark style="color:$warning;">**Application Allow-listing:**</mark>
  * Only explicitly approved applications are permitted to execute on the device.
  * All other unapproved applications are blocked by default.
  * Users must not be able to install any application that is unsigned or has an invalid signature.
* <mark style="color:$warning;">**Application Sandboxing**</mark> <mark style="color:$warning;"></mark><mark style="color:$warning;">(natively built-in and acceptable by default for mobile OSs)</mark><mark style="color:$warning;">**:**</mark>
  * All application code is forced to run within an isolated environment.
  * The sandbox prevents the application from interacting with other applications, data, or core operating system functions without explicit user permission.

***

## Security Update Management

<mark style="color:$info;">**Objective:**</mark> To ensure that all software and operating systems are kept up to date so that known vulnerabilities are patched before attackers can exploit them.

#### Requirements:

* <mark style="color:$warning;">**Supported Software:**</mark> All operating systems, applications, and firmware must be licensed and supported by the vendor (they still receive security updates). If it is unsupported, it is an automatic failure.
* <mark style="color:$warning;">**Unsupported Software:**</mark> Unsupported software must be entirely removed from in-scope devices.
* <mark style="color:$warning;">**The 14-Day Rule:**</mark> All security updates labelled by the vendor as "High" or "Critical" severity (or with a CVSS v3 score of 7.0 and above) must be applied within 14 days of release.
* <mark style="color:$warning;">**Auto-Updates:**</mark> Where possible, automatic updates should be enabled to ensure compliance and assist in meeting the 14-day requirement.
