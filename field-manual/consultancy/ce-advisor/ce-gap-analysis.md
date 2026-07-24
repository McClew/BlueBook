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

# CE Gap Analysis

Performing Gap Analysis is the core technical activity of a Cyber Advisor. It is the process of mapping an organisation's _actual_ IT environment against the required technical controls of the Cyber Essentials standard to identify vulnerabilities and compliance failures.

Unlick a formal CE+ auditor, a Cyber Advisor conducts this analysis collaboratively. Advisors are not to assessing the client, they discover the reality of the organisations security hygiene and build a roadmap to compliance.

***

## The Gap Analysis Process

A successful gap analysis follows three distinct phases:

### 1. Information Gathering (Discovery)

An Advisor cannot assume what is written in the company IT policy matches reality. Advisors need to identify if any shadow IT is in place, and if there are any "workarounds" that staff use.

* **Interview Broadly:** Speak to business leaders, IT and non-technical end-users.
* **Ask Open-ended Questions:** Instead of asking "Do you use a VPN?", ask "How do you access the payroll system when you work from home?"
* **Review Existing Documentation:** Look at the organisations asset registers, cloud subscriptions and user lists.

### 2. Asset Mapping (Defining Scope)

The Advisor must identify every piece of hardware, software and cloud service that touches the business. This leads to defining [the-boundary-and-scoping.md](the-boundary-and-scoping.md "mention").

### 3. Control Evaluation

The Advisor needs to methodically evaluate the scoped assets against the Five Techincal Controls:

1. **Firewalls/Routers:** Are default passwords changed? Are unused ports blocked?
2. **Secure Configuration:** Are default accounts removed? Is auto-run disabled?
3. **User Access Control:** Does everyone have a unique login? Is MFA enforced on all cloud services?
4. **Malware Protection:** Is anti-malware active and updating?
5. **Security Update Management:** Are all OS and apps supported? Are critical/high patches applied within 14 days?

