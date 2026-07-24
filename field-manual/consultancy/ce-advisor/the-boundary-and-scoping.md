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

# The Boundary & Scoping

Before a Cyber Advisor can assess if a company meets the five technical controls, they must accurately define _what_ needs to be assessed. This is known as defining the scope and the boundary.

***

## Defining the Boundary

The scope of a Cyber Essentials assessment is defined by the network boundary. Everything inside the boundary that has access to the internet is **IN SCOPE**.

{% hint style="info" icon="exclamation" %}
#### The Golden Rule of Scoping

If a device accesses organisational data or services and it connects to the internet, it is **IN SCOPE**.
{% endhint %}

### Whole Organisation vs. Sub-set

The NCSC strongly recommends scoping the "Whole Organisation." However, a company can assess a "sub-set", - for example, just the HR department - but only if that sub-set is completely segregated from the rest of the network via a firewall or VLAN.

### Out of Scope

Devices that do not access organisational data or devices that are completely disconnected from the internet are **OUT OF SCOPE**.

***

## Remote Working & BYOD

In most modern workplaces the boundary is no longer just the office network, it now extends to wherever the staff are working.

### BYOD

If a staff member uses their personal device (e.g. laptop or mobile) to access company data, that personal device is **IN SCOPE**.

{% hint style="info" %}
#### Advising the Client

Business owners often take issue with this scoping because they cannot enforce remote management software, such as RMM or MDM, on personal devices.

Advisors should suggest:&#x20;

* securing the personal devices to CE standards, or;
* implementing technical policies that block personal devices from accessing company data.
{% endhint %}

### Remote Working

Under the CE v3.3 standard,, a home workers ISP-provided router is **OUT OF SCOPE**.

Because the home router is out of scope, the boundary firewall shifts to the device itself. Therefore, a remote worker's laptop **MUST** have a software firewall (host-based firewall) enabled and configured to block unapproved incoming connections.

***

## Cloud Services & SaaS

Most SMEs rely heavily on cloud services. Advisors must understand the **Share Responsibility Model** and apply the **NCSC Cloud Security Principles**.

### Software as a Service (SaaS)

The cloud provider manages the infrastructure, OS, and application. The business is only responsible for:

* User Access Control (enforcing strong passwords and MFA) and;
* Secure Configuration (setting appropriate permissions within the app).

### Platform as a Service (PaaS)

The business might deploy their own apps. The organisation is responsible for:

* user access,&#x20;
* application configuration, and;&#x20;
* potentially some malware protection.

### Infrastructure as a Service (IaaS)

The business rents a virtual server (e.g., an AWS EC2 instance). Because the business manages the operating system, **ALL** 5 CE technical controls apply to that virtual server:

* Firewall
* Secure Config
* Updates
* Malware Protection
* Access Control
