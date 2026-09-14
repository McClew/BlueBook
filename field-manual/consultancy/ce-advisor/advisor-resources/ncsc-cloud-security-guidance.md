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

# NCSC Cloud Security Guidance

The **NCSC Cloud Security Guidance** collection explains how to choose, configure, and use cloud services securely. [Source](https://www.ncsc.gov.uk/collection/cloud)

***

## Why This Guidance Matters

Cyber Advisors need this because nearly every SME client relies on SaaS (Google Workspace, Microsoft 365, Xero, etc.) rather than running their own servers - the [the-boundary-and-scoping.md](../the-boundary-and-scoping.md "mention") section already establishes _which_ CE controls a client is responsible for under the Shared Responsibility Model. This guidance goes one level deeper: it's what you'd point to if a client asks "how do I actually judge whether our cloud provider itself is any good?"

The NCSC publishes two tiers of assessment:

* <mark style="color:$info;">**The full 14 Cloud Security Principles:**</mark> aimed at larger organisations, the public sector, or anyone handling sensitive/OFFICIAL data when choosing between enterprise cloud providers. Heavier and more formal than almost any Cyber Advisor client will need.
* <mark style="color:$info;">**The Lightweight Approach to Cloud Security:**</mark> a rapid, reliable assessment built for organisations _not_ holding sensitive data - i.e. the overwhelming majority of Cyber Advisor clients. This is the one worth knowing well.

{% hint style="info" %}
**Not a CE Requirement, But Useful Due Diligence**

None of the checks below are formally assessed by Cyber Essentials. CE only requires MFA and Secure Configuration for the cloud services a client actually uses (see [the-five-technical-controls.md](../the-five-technical-controls.md "mention")). This guidance is a due-diligence layer _on top of_ CE - useful when a client is choosing a new provider, or asks "is our cloud provider actually secure?"
{% endhint %}

***

## The Lightweight Cloud Security Framework

Four areas, each with simple yes/no questions to put to a provider — no deep technical research required. [Source](https://www.ncsc.gov.uk/collection/cloud/the-cloud-security-principles/lightweight-approach-to-cloud-security)

### 1. Data Encryption

| What to ask the provider                                                                           | Overlaps a CE control?                                                   |
| -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| "Does the service protect data in transit using TLS 1.2+, with correctly configured certificates?" | _Not a CE requirement._ CE doesn't assess transport encryption directly. |
| "Is data encrypted when stored on disk?"                                                           | _Not a CE requirement._                                                  |

### 2. Authentication and Access Control

| What to ask the provider                                                                  | Overlaps a CE control?                                                                                                                                                                                                                                                            |
| ----------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| "Are internal and external APIs protected by authentication?"                             | _Not directly CE_ - relevant if a client integrates other tools via API.                                                                                                                                                                                                          |
| "Can MFA be mandated for all users, and is it at least available on privileged accounts?" | <i class="fa-siren-on" style="color:$danger;">:siren-on:</i> <mark style="color:$danger;">**Overlaps User Access Control:**</mark> CE already mandates MFA for cloud services and admin accounts — this checks whether the \*provider itself\* technically supports enforcing it. |
| "Does the service support Single Sign-On to our identity provider?"                       | _Not a CE requirement_ - a best-practice enabler for consistent access control.                                                                                                                                                                                                   |
| "Are there separate privileged/administrative and standard user roles?"                   | <i class="fa-siren-on" style="color:$danger;">:siren-on:</i> <mark style="color:$danger;">**Overlaps User Access Control:**</mark> CE requires admin accounts to be used only for admin tasks — this checks the provider actually supports that separation.                       |

### 3. Security Logging and Incident Management

| What to ask the provider                                                                     | Overlaps a CE control?                                                                                                                                                        |
| -------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| "Does the service collect security-critical logs (authentication attempts, config changes)?" | _Not a CE requirement_ - but the exact evidence source CE+ auditors use to verify MFA and access control (see [ce+-technical-audit.md](../ce+-technical-audit.md "mention")). |
| "Are logs made available to us, e.g. for export?"                                            | _Not a CE requirement._                                                                                                                                                       |
| "Do you have an incident response process, and a policy for applying security updates?"      | _Not a CE requirement_ - though relevant context if a client is nervous about provider reliability.                                                                           |
| "Do you have a documented vulnerability disclosure process?"                                 | _Not a CE requirement._                                                                                                                                                       |

### 4. Governance

| What to ask the provider                                                                    | Overlaps a CE control?                                                                                            |
| ------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| "Do you publish a privacy policy covering third-party data sharing?"                        | _Not a CE requirement_ - a GDPR/data-protection concern, outside CE's boundary.                                   |
| "Where is our data processed and stored, and where is the company legally based?"           | _Not a CE requirement._                                                                                           |
| "Do you publish a security whitepaper, audit report, or good-practice configuration guide?" | _Not a CE requirement_ - but the practical source for correctly configuring Secure Configuration on that service. |

{% hint style="warning" %}
**Sensitive Workloads**

If a client is going to process large amounts of personal data, commercially sensitive information, or plug the service into a larger trusted system, the lightweight approach isn't enough - point them to the full 14 principles instead.
{% endhint %}

***

## Advising the Client

Two moments this is actually useful in practice:

* <mark style="color:$info;">**Choosing a new provider:**</mark> run through the four lightweight-approach areas as a quick due-diligence pass before a client signs up to a new SaaS tool.
* <mark style="color:$info;">**Responding to "is this actually secure?"**</mark> — rather than a vague reassurance, these are concrete, plain-English questions a non-technical business owner could put to a salesperson directly.

Frame this the same way as any other advice per effective-communication — as due diligence that builds confidence, not as a compliance requirement they're failing.
