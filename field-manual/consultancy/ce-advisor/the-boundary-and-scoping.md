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

# The Boundary & Scoping

Before a Cyber Advisor can assess if a company meets the five technical controls, they must accurately define _what_ needs to be assessed. This is known as defining the scope and the boundary.

***

## Defining the Boundary

The scope of a Cyber Essentials assessment is defined by the boundary the organisation declares: the business unit managing it, the network boundary, and the physical location.

<i class="fa-siren-on" style="color:red;">:siren-on:</i> The scope must be agreed with the Certification Body before the assessment begins.

{% hint style="danger" %}
#### In-scope by Default

Start from the assumption that everything is <mark style="color:$success;">**IN SCOPE**</mark> unless it has been specifically excluded using a **sub-set**.
{% endhint %}

{% hint style="info" icon="exclamation" %}
#### The Golden Rule of Scoping

If a device accesses organisational data or services and it connects to the internet, it is <mark style="color:$success;">**IN SCOPE**</mark>.
{% endhint %}

### Whole Organisation vs. Sub-set

A **sub-set** is part of the organisation’s network that is segregated from the rest by a **firewall or VLAN**. Segregation must happen at Layer 2 or 3; user groups and micro-segmentation do not count. A sub-set can be used to mark either what’s in scope or what’s out of scope.

There are three possible outcomes:

| Scope type                                          | When it applies                                                                                                                                                                            | Certificate wording                                                      | Included cyber insurance |
| --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------ |
| **Whole Organisation**                              | Nothing excluded                                                                                                                                                                           | “Whole Organisation”                                                     | Eligible                 |
| **Whole Organisation with an out-of-scope sub-set** | Excluded devices sit in a sub-set with **all inbound and outbound internet traffic blocked** at its boundary. Used for unsupported or unpatchable devices (legacy OS, OT/CNC controllers). | “Whole Organisation”                                                     | Eligible                 |
| **Partial scope**                                   | The excluded part **still has internet access** (e.g. a development network, or certifying only one department)                                                                            | Exclusion named, e.g. “Whole Organisation excluding development network” | Not eligible             |

* The NCSC strongly recommends Whole Organisation.
* Any partial scope must be justified to the assessor.
* A CE+ assessment must use the same scope as the CE certificate it follows.

### Out of Scope

A device is <mark style="color:$danger;">**OUT OF SCOPE**</mark> if:

* it does not access organisational data or services, **or**
* it sits in a defined sub-set that blocks all inbound and outbound internet traffic at the sub-set boundary.

Also out of scope:

* Home workers’ ISP-provided routers, unless the organisation supplied the router.
* Phones used only for native calls, native texts, or as an MFA device.

<div data-with-frame="true"><figure><img src="../../../.gitbook/assets/image (26).png" alt=""><figcaption><p>Example of an allowed sub-set for a legacy device from official IASME <a href="https://iasme.atlassian.net/wiki/pages/viewpage.action?pageId=2977595427">wiki</a>.</p></figcaption></figure></div>

**Can never be excluded:**

* Cloud services.
* Staff BYOD that accesses organisational data or services.
* End-user devices as a whole (a scope without them isn’t acceptable).

{% hint style="info" icon="network-wired" %}
#### Traffic Across the Sub-set Boundary

A limited internal rule between an out-of-scope sub-set and in-scope devices doesn’t bring the sub-set back into scope by itself, as long as all internet traffic is blocked.

However, assessors may scrutinise it. Keep it tightly scoped (specific source, destination and port, deny everything else), document the business need, and describe it to the Certification Body when agreeing the scope.
{% endhint %}

{% hint style="info" icon="memo" %}
#### Evidence to Keep for a De-scoped Device

* A scope statement
* A network diagram showing the sub-set
* Firewall/VLAN rule exports
* An asset list marking the device as out of scope
* A test showing the device can’t reach the internet
{% endhint %}

***

## Remote Working & BYOD

In most modern workplaces the boundary is no longer just the office network, it now extends to wherever the staff are working.

### BYOD

If a staff member uses their personal device (e.g. laptop or mobile) to access company data, that personal device is <mark style="color:$success;">**IN SCOPE**</mark>.

{% hint style="info" %}
#### Advising the Client

Business owners often take issue with this scoping because they cannot enforce remote management software, such as RMM or MDM, on personal devices.

Advisors should suggest:&#x20;

* securing the personal devices to CE standards, or;
* implementing technical policies that block personal devices from accessing company data.
{% endhint %}

### Remote Working

Under the CE v3.3 standard, a home workers ISP-provided router is <mark style="color:$danger;">**OUT OF SCOPE**</mark>.

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
