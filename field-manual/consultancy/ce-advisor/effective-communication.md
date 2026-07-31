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

# Effective Communication

Cyber Advisors primary value is acting as a translator between the strict technical requirements of the Cyber Essentials standard and the day-to-day realities of SMEs. The Cyber Advisor Standard explicitly calls for Advisors to maintain a <mark style="color:$info;">**Professional**</mark>, <mark style="color:$info;">**Collaborative**</mark> and <mark style="color:$info;">**Non-Judgemental**</mark> approach across all interactions.

***

## Securing Buy-in Through Translation

When presenting a gap analysis report to a client, quoting the CE standard verbatim: "You fail to meet the requirement for application sandboxing" will alienate them. Instead, we must root the explanation in the business risks outline in the [ncsc-small-organisation-guide.md](advisor-resources/ncsc-small-organisation-guide.md "mention"). Explain _why_ using the Guide, and implement the _how_ using the CE Standard.

> "If you ensure all your equipment is configured to receive automatic updates, you will be protected against the majority of cyber attacks."
>
> \- [ncsc-small-organisation-guide.md](advisor-resources/ncsc-small-organisation-guide.md "mention"): Protecting your organisation from malware

When a client pushes back on the cost or disruption of an upgrade, frame the CE technical requirement (Security Update Management) as the solution to the business risk (malware disrupting their operations).

### The Jargon Trap

Technical professionals often suffer from the "curse of knowledge," casually using acronyms and specific IT terms that confuse business owners. When assessing a business we must strip away terms like "SSO", "firewall rulesets", "subnets", and "heuristics."

Instead of talking about _how_ the technology works under the hood, focus on _what_ the technology does for the business. A key indicator that you are using jargon is if the term requires a prerequisite understanding of networking or computer science to make sense.

### The Translation Framework

To successfully communicate with business leaders, use the "<mark style="color:$info;">So What?</mark>" framework for every Cyber Essentials control you discuss. State the requirement, ask yourself "<mark style="color:$info;">so what?</mark>", and explain the business impact.

For example, instead of saying "<mark style="background-color:$danger;">You need to patch vulnerabilities with a CVSS score of 7 or above within 14 days,</mark>" we translate it to: "<mark style="background-color:$success;">We need to update your software within two weeks of a high-risk flaw being discovered, otherwise hackers can use that known flaw to break into your systems.</mark>"



***

## Communicating with SME Business Leaders

Business leaders will focus on three things: <mark style="color:$warning;">**Cost**</mark>, <mark style="color:$warning;">**Business Operations**</mark> and <mark style="color:$warning;">**Reputation**</mark>.

#### Key Strategies:

* <mark style="color:$info;">**Translate Technical Flaws into Business Risk:**</mark> Instead of stating: \
  "<mark style="background-color:$danger;">This laptop is running Windows 10, which fails the CE secure configuration control,</mark>" \
  say: "<mark style="background-color:$success;">One of your laptops is running outdated software that no longer recieves security updates. This makes it an easy target for hackers, which could lead to a data breach or ransomware shitting down your operations.</mark>"
* <mark style="color:$info;">**Use the NCSC Small Organisations Guide:**</mark> Frame advice using the plain-English pillars of the NCSC guide.
* <mark style="color:$info;">**Be Sympathetic to Operations:**</mark> Acknowledge that security changes cause friction. When proposing remediations, explain _why_ it's necessary for their specific goal.
* <mark style="color:$info;">**Provide Actionable Summaries:**</mark> Leadership needs clear options, present the gap, the risk, the recommended fix and the estimated operational impact.

{% hint style="info" %}
#### Use Objective Alignment

If a disagreement with leadership occurs, use a technique called **Objective Alignment**.

Much like relying on a standard with an advisor, handling leadership requires removing personal opinions and anchoring the conversation to **business data, corporate goals, or external regulations**.

1. <mark style="color:$primary;">**Defuse & Mollify:**</mark> Lower the intensity of the conversation before the conflict can start. Find a way of agreeing with their statement and avoid being drawn into an argument.\
   _"<mark style="background-color:$success;">I completely agree that accelerating the product launch is our top priority.</mark>"_
2. <mark style="color:$primary;">**Shift to a Shared Goal:**</mark> After validating their own objectives or opinions, find a way to combine your advice/goal with theirs:\
   _"<mark style="background-color:$success;">To ensure we don't face costly compliance delays at the finish line, the SOC 2 framework requires us to complete the penetration test before we go live. Let's look at how we can schedule that concurrently.</mark>"_
3. <mark style="color:$primary;">**Anchor to Risk Appetite:**</mark> Leadership is responsible for managing organisational risk, not just technical details. Translate the technical conflict into financial or operation impact.\
   _"<mark style="background-color:$success;">I understand your goal is to minimise user friction by removing multi-factor authentication. However, doing so breaches our current cyber insurance policy requirements, which would invalidate our coverage in a breach. Should we schedule a review with the risk committee to evaluate this gap?</mark>"_
4. <mark style="color:$primary;">**Separate Person from Process:**</mark> When leaders face a pushback, they may perceive it as a challenge to their authority. Maintain neutrality by blaming the process or the criteria. Use objective data, metrics, or third-party audits as the "bad guy" so you and the leader remain on the same team.\
   _"<mark style="background-color:$success;">The latest performance metrics show the system cannot handle this traffic load without a load balancer. It isn't a matter of design preference; the hardware limitations dictate that we must scale up to prevent a Q3 outage.</mark>"_
{% endhint %}

***

## Communicating with Non-Technical Personnel

The primary goals when communicating with non-technical staff are usually information gathering and education. An Advisor needs to find out how they actually work, which often differs from official company policy.

#### Key Strategies:

* <mark style="color:$info;">**Active Listening & Open-Ended Questions:**</mark> Avoid technical interrogations (e.g., "<mark style="background-color:$danger;">Do you use a VPN or split-tunnelling?</mark>"). Instead, ask workflow questions: "<mark style="background-color:$success;">Can you walk me through how you check your work emails from home?</mark>"
* <mark style="color:$info;">**Be Non-Judgemental:**</mark> Staff will hide insecure workarounds if they feel they will be reprimanded. If an admin admits they email sensitive payroll data to their personal Gmail to print at home, do not scold them. Thank them for the information, and not is as a gap in boundary scoping and data handling that needs to be addressed through policy and secure alternatives.
* <mark style="color:$info;">**Demystify the "Why":**</mark> When an Advisor is guiding personnel through a remediation step, explain _why_ it helps them personally.

***

## Communicating with  IT Providers

Communicating with internal or external IT can often be a delicate communication scenario. The IT provider may feel defensive, viewing the gap analysis as an audit or critique of their work.

#### Key Strategies:

* <mark style="color:$info;">**Adopt a Collaborative Approach:**</mark> The Cyber Advisor Standard demands Advisors work _jointly_ with third-parties. Frame the engagement as a partnership to help the mutual client achieve certification, not as an inspection of the IT provider's competence.
* <mark style="color:$info;">**Rely on the Standard Neutrally:**</mark> When challenged on a control, Advisors should avoid being drawn into opinion-based arguments about security. Neutrally point to the standard:\
  "<mark style="background-color:$success;">I completely agree your perimeter is strong, but the Cyber Essentials Requirements for IT Infrastructure specifically mandates software firewalls on all in-scope devices to protect them when they leave the corporate network.</mark>"
* <mark style="color:$info;">**Speak their Language:**</mark> Unlike with business leaders, Advisors should use precise technical terminology in these scenarios to ensure that remediation is carried out exactly as the CE standard requires.
* <mark style="color:$info;">**Acknowledge their Constraints:**</mark> MSPs have other clients and tight SLAs. Advisors must work with them to plan remediation sympathetically.

{% hint style="info" %}
#### Relying on the Standard

When challenged on required remediation steps, frame the response like below:

1. <mark style="color:$primary;">**Defuse & Mollify:**</mark> Lower the intensity of the conversation before the conflict can start. Find a way of agreeing with their statement and avoid being drawn into an argument.
2. <mark style="color:$primary;">**Pivot to the Standard:**</mark> Use the CE standard and requirements to explain that the control is _required_. Ensure the statement is expressed neutrally and without judgement.
3. <mark style="color:$primary;">**Explain the "Why":**</mark> Explain the importance of the control in regards to the CE standard and why it is a requirement.
{% endhint %}

***

## Examples of Communication

### Example 1: Addressing Unsupported Operating Systems

The gap analysis shows a Dell Latitude 5450 running Windows 8.1 Pro. This fails the CE _Security Update Management_ and _Secure Configuration_ controls, as the OS is end-of-life and no longer receives security updates.

{% stepper %}
{% step %}
#### Identify the Small Business Guide hook

_Keeping devices safe._

Mentally map the CE failure to the Small Business Guide's advice on "Keeping your smartphones and tablets (and laptops) safe" - specifically the rule to switch on automatic updates and use supported software.
{% endstep %}

{% step %}
#### Translate the technical risk to business risk

Instead of saying "Windows 8.1 fails CE requirement 4.2," say:&#x20;

> "Nia, your Dell laptop running Windows 10 is no longer supported by Microsoft. This means if a new flaw is discovered, Microsoft won't fix it, leaving StayUp vulnerable to attacks that could disrupt your building projects."
{% endstep %}

{% step %}
#### Propose the CE-compliant remediation

Offer a proportionate solution:

> "To meet the prime contractor's requirement for Cyber Essentials, we need to either upgrade this laptop to Windows 11 if the hardware supports it, or replace the device."
{% endstep %}
{% endstepper %}

### Example 2: Implementing Strict Access Controls

The gap analysis shows Richard and Greg share a single local administrator account on the office PCs, and they use simple passwords.

{% stepper %}
{% step %}
#### Identify the Small Business Guide hook

_Using passwords to protect your data._

Map this to the Guide's advice on password management, multi-factor authentication, and ensuring staff only have the access they need to do their jobs.
{% endstep %}

{% step %}
#### Explain the risk to the owner

> "Currently, Richard and Greg are using accounts that can install any software on your systems. If they click a bad link, the malware gets those same administrative powers. We need to protect your data by separating their daily work from administrative tasks."
{% endstep %}

{% step %}
#### Present the remediation plan

> "We will set up standard user accounts for their daily tasks. We will also implement a strict password policy - such as using three random words - and enforce Multi-Factor Authentication (MFA) on your cloud services to lock down access."
{% endstep %}
{% endstepper %}
