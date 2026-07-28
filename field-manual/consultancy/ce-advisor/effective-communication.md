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
   &#xNAN;_"<mark style="background-color:$success;">I completely agree that accelerating the product launch is our top priority.</mark>"_
2. <mark style="color:$primary;">**Shift to a Shared Goal:**</mark> After validating their own objectives or opinions, find a way to combine your advice/goal with theirs:\
   &#xNAN;_"<mark style="background-color:$success;">To ensure we don't face costly compliance delays at the finish line, the SOC 2 framework requires us to complete the penetration test before we go live. Let's look at how we can schedule that concurrently.</mark>"_
3. <mark style="color:$primary;">**Anchor to Risk Appetite:**</mark> Leadership is responsible for managing organisational risk, not just technical details. Translate the technical conflict into financial or operation impact.\
   &#xNAN;_"<mark style="background-color:$success;">I understand your goal is to minimise user friction by removing multi-factor authentication. However, doing so breaches our current cyber insurance policy requirements, which would invalidate our coverage in a breach. Should we schedule a review with the risk committee to evaluate this gap?</mark>"_
4. <mark style="color:$primary;">**Separate Person from Process:**</mark> When leaders face a pushback, they may perceive it as a challenge to their authority. Maintain neutrality by blaming the process or the criteria. Use objective data, metrics, or third-party audits as the "bad guy" so you and the leader remain on the same team.\
   &#xNAN;_"<mark style="background-color:$success;">The latest performance metrics show the system cannot handle this traffic load without a load balancer. It isn't a matter of design preference; the hardware limitations dictate that we must scale up to prevent a Q3 outage.</mark>"_
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
