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

# NCSC Small Organisation Guide

The **NCSC Small Organisations Guide to Cyber Security** provides a baseline of 5 non-technical categories that you can use as an objective standard when leadership pushes back on security decisions. [Source](https://www.ncsc.gov.uk/collection/small-organisations-guide-to-cyber-security)

***

## Why This Guide Matters

Cyber Advisors must be able to translate strict technical controls into non-technical, actionable business advice. The NCSC Small Business Guide provides the plain-English vocabulary to explain why Cyber Essentials (CE) controls matter to a small business owner, ensuring they understand the risks and agree to the remediation work.

It is vital to frame advice sympathetically to their reality:

* There are 5.5 million small organisations in the UK (between 0 and 49 employees).
* No business is too small to be a target; 50% small businesses suffer a cyber incident every year.
* Improving security does not require them to be technical experts.
* Cyber security is everyone’s business, meaning responsibility should not fall on a single person.

***

## The 5 Core Categories & Leadership Scripts

The guide simplifies cyber security into five understandable recommendations. When presenting gap analysis findings to leadership, frame your advice around these pillars rather than dry technical specifications.

### Secure your email

Email is the gateway to the business. This focuses on protecting email accounts with strong passwords, Multi-Factor Authentication (MFA), and being cautious about what is sent.

<table><thead><tr><th width="257.33331298828125">Recommendation</th><th>CE Requirement?</th></tr></thead><tbody><tr><td><strong>Enable MFA</strong></td><td><i class="fa-siren-on" style="color:$danger;">:siren-on:</i> <strong>CE Requirement</strong>: Multi-Factor Authentication (MFA) must be enabled for all users accessing cloud services.<br><em>(Maps to: User Access Control)</em></td></tr><tr><td><strong>Use a strong, separate password for your email</strong></td><td><i class="fa-siren-on" style="color:$danger;">:siren-on:</i> <strong>CE Requirement:</strong> Passwords must meet specific CE criteria (e.g., at least 8 characters long when combined with MFA or anti-guessing measures, or 12 characters minimum). Passwords cannot be shared across different services. <br><em>(Maps to: User Access Control)</em></td></tr><tr><td><strong>Be cautious with what you share and send</strong></td><td><em>Not a CE Requirement.</em> CE does not formally assess user awareness or data loss prevention.</td></tr></tbody></table>

### Secure your important online accounts

Protecting access to crucial services (like banking, social media, or IT administration) using MFA, password managers, and ensuring staff only have the access they need to do their jobs.

<table><thead><tr><th width="257.33331298828125">Recommendation</th><th>CE Requirement?</th></tr></thead><tbody><tr><td><strong>Enable MFA</strong></td><td><i class="fa-siren-on" style="color:$danger;">:siren-on:</i> <strong>CE Requirement</strong>: Multi-Factor Authentication (MFA) must be enabled for all users accessing cloud services.<br><em>(Maps to: User Access Control)</em></td></tr><tr><td><strong>Use a Password Manager</strong></td><td><p><em>Best Practice (Helps pass CE):</em> While not strictly required, CE encourages password managers because they help users comply with the strict CE rules of having long, unique passwords for every service without having to write them down securely.</p><p><em>(Maps to: User Access Control)</em></p></td></tr><tr><td><strong>Create strong passwords using 3 random words</strong></td><td><em>Best Practice (Helps pass CE):</em> CE mandates minimum password lengths and complexity. The NCSC's "3 random words" strategy is their recommended way to help users generate passwords that exceed the CE 8-to-12 character minimums easily.<br><em>(Maps to: User Access Control)</em></td></tr><tr><td><strong>Remove access for staff who have left or no longer need it</strong></td><td><p><i class="fa-siren-on" style="color:$danger;">:siren-on:</i> <strong>CE Requirement:</strong> You must have a process to create and approve accounts, and specifically, to remove or disable accounts when they are no longer required (e.g., when an employee leaves).</p><p><em>(Maps to: User Access Control)</em></p></td></tr></tbody></table>

### Protecting your devices

Keeping smartphones, laptops, and tablets safe by applying security updates, turning on built-in security features (like firewalls and antivirus), and using screen locks.

<table><thead><tr><th width="257.33331298828125">Recommendation</th><th width="466.66668701171875">CE Requirement?</th></tr></thead><tbody><tr><td><strong>Switch on your firewall</strong></td><td><p><i class="fa-siren-on" style="color:$danger;">:siren-on:</i> <strong>CE Requirement</strong>: A software firewall must be enabled and configured on every in-scope device to protect it when it leaves the corporate network, alongside a boundary firewall for the office.</p><p><em>(Maps to: Firewalls and Routers)</em></p></td></tr><tr><td><strong>Apply updates promptly (Turn on automatic updates)</strong></td><td><p><i class="fa-siren-on" style="color:$danger;">:siren-on:</i> <strong>CE Requirement:</strong> All software, apps, and operating systems must be kept up to date. Any "High" or "Critical" security updates must be applied within 14 days of release.</p><p><em>(Maps to: Security Update Management)</em></p></td></tr><tr><td><strong>Use Antivirus / Anti-malware software</strong></td><td><p><i class="fa-siren-on" style="color:$danger;">:siren-on:</i> <strong>CE Requirement:</strong> Devices must be protected from malicious software. For most standard OSs (Windows/macOS), this means running updated anti-malware software (like Windows Defender) that scans files upon access.</p><p><em>(Maps to: Malware Protection)</em></p></td></tr><tr><td><strong>Lock your devices (PIN, password, or biometrics)</strong></td><td><p><i class="fa-siren-on" style="color:$danger;">:siren-on:</i> <strong>CE Requirement:</strong> All in-scope devices must require a password, PIN, or biometric authentication to unlock them.</p><p><em>(Maps to: User Access Control / Secure Configuration)</em></p></td></tr><tr><td><strong>Remove unused software and apps</strong></td><td><p><i class="fa-siren-on" style="color:$danger;">:siren-on:</i> <strong>CE Requirement:</strong> Only approved software should be installed. Any unused applications or services must be removed or disabled to reduce the attack surface.</p><p><em>(Maps to: Secure Configuration)</em></p></td></tr></tbody></table>

### Backing up your data

Ensuring critical business data is copied and stored securely, separate from the main network, to recover from ransomware, theft, or hardware failure.

{% hint style="info" %}
#### User Awareness Caveat

A Cyber Advisor should advise clients to train their staff, but a lack of phishing training will not cause them to fail a CE assessment.
{% endhint %}

<table><thead><tr><th width="257.33331298828125">Recommendation</th><th width="466.66668701171875">CE Requirement?</th></tr></thead><tbody><tr><td><strong>Identify what data is critical to the business</strong></td><td><em>Not a CE Requirement.</em></td></tr><tr><td><strong>Keep your backups separate from your computer and network (Offline/Cold storage or secure cloud)</strong></td><td><em>Not a CE Requirement:</em> A company with zero backups will still pass Cyber Essentials if their technical controls are in place.</td></tr><tr><td><strong>Test your backups regularly to ensure they work</strong></td><td><em>Not a CE Requirement:</em> While backups are critical for business survival and are a massive part of NCSC guidance, Cyber Essentials does not assess backups.</td></tr></tbody></table>

### Spotting cyber attacks

Training staff to recognise phishing emails, suspicious messages, and knowing what to do if they click a bad link (fostering a blame-free reporting culture).

{% hint style="info" %}
#### Backups Caveat

A Cyber Advisor should advise clients to back up their data, but a lack of backups will not cause them to fail a CE assessment.
{% endhint %}

<table><thead><tr><th width="257.33331298828125">Recommendation</th><th width="466.66668701171875">CE Requirement?</th></tr></thead><tbody><tr><td><strong>Train staff to spot the signs of phishing</strong></td><td><em>Not a CE Requirement:</em> Cyber Essentials is a technical baseline standard. It assesses the configuration of IT infrastructure, not the cybersecurity awareness of the staff or the presence of training policies.</td></tr><tr><td><strong>Create a blame-free reporting culture</strong></td><td><em>Not a CE Requirement:</em> Cyber Essentials is a technical baseline standard. It assesses the configuration of IT infrastructure, not the cybersecurity awareness of the staff or the presence of training policies.</td></tr><tr><td><strong>Use the NCSC's Suspicious Email Reporting Service (SERS)</strong></td><td><em>Not a CE Requirement:</em> Cyber Essentials is a technical baseline standard. It assesses the configuration of IT infrastructure, not the cybersecurity awareness of the staff or the presence of training policies.</td></tr></tbody></table>
