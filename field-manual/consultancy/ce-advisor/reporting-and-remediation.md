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

# Reporting & Remediation

Cyber Advisors must report the found technical gaps in a report. The real value to clients lies in how these vulnerabilities are reported to business leaders and how they are aided in remediating the issues.

The NCSC Cyber Advisor Standard mandates specific approaches to reporting and remediation.

***

## Gap Analysis Report

After conducting the Gap Analysis assessment, the Advisor must present a formal report to the senior leadership team. This report must not read like an automated IT scan; it must translate technical findings into business risk.

#### The 4-Part Reporting Structure

To ensure the report is actionable and provides real value to clients, structure every failed control using this logical flow:

1. <mark style="color:$info;">**The Observation:**</mark>
   * State the facts clearly based on your discovery.
   * _Example:_ "Three members of the sales team are using personal, unmanaged mobile phones to access the company's Google Workspace."
2. <mark style="color:$info;">**The Compliance Gap:**</mark>
   * State the specific Cyber Essentials requirement that was not met.
   * _Example:_ "Under Cyber Essentials, any device accessing company data must enforce a screen lock, run supported software, and restrict malicious apps. We currently cannot verify these controls on personal devices."
3. <mark style="color:$info;">**The Business Risk:**</mark>
   * Translate the gap into a business threat using the [ncsc-small-organisation-guide.md](advisor-resources/ncsc-small-organisation-guide.md "mention") pillars.
   * _Example:_ "If a sales rep loses their phone, or if it gets infected by a malicious app, attackers could gain access to your company emails and client data, leading to a severe data breach."
4. <mark style="color:$info;">**The Actionable Recommendation:**</mark>
   * Provide clear, cost-aware options for the leadership to choose from.
   * _Example:_ "Option A: We implement Conditional Access to block personal phones, forcing staff to only use work laptops. Option B: We require staff to enrol their personal phones into a lightweight Mobile Device Management (MDM) profile to enforce screen locks."

***

## Sympathetic Remediation Planning

Once leadership approves the recommendations, the Advisor must work with internal IT staff, an external Managed Service Provider (MSP), or the staff themselves to deploy the changes.

The Cyber Advisor standard mandates a Professional, Collaborative, and Non-Judgemental approach.

**Key Strategies for Sympathetic Planning:**

* <mark style="color:$info;">**Understand Business Priorities:**</mark> Do not deploy disruptive changes during critical business operations. If MFA registration needs to be applied to for all users, do not schedule it on the day the finance team processes payroll. Propose a phased rollout.
* <mark style="color:$info;">**Acknowledge IT Workloads:**</mark> If working with an MSP or internal IT, treat them as partners, not subjects of an audit. Agree on timelines that respect their existing SLA commitments.
* <mark style="color:$info;">**Find Cost-Effective Paths:**</mark> If a business is running a legacy, unsupported Windows 10 machine to operate a vital, expensive piece of manufacturing hardware, do not simply tell them to "buy a new machine." Work with IT to sympathetically remove the machine from scope (e.g., by completely air-gapping it from the internet or placing it behind a strict internal firewall).

### Prioritising Remediation & Minimising Disruption

If a business owner is provided unsympathetic advice to implement all fixes simultaneously on a Monday morning without proper consideration of the businesses needs the organisation could be operationally affected and causing a loss of trust.

To prevent this, use the Impact vs. Disruption Matrix to phase the remediation plan.

#### The Two Core Factors

When looking at a list of CE failures, evaluate each one against two questions:

1. <mark style="color:$info;">Security Risk:</mark> How likely is this specific vulnerability to be exploited, and how bad would it be if it was? (e.g., No MFA on internet-facing email is a massive, immediate risk).
2. <mark style="color:$info;">Business Disruption:</mark> How much will fixing this impact the end-user's ability to do their daily job? (e.g., Replacing a core software platform is highly disruptive; changing a router admin password is zero disruption).

#### The 4-Phase Remediation Framework

When presenting the remediation plan to a client, we should group the required fixes into these four phases. This shows the client you respect their operational uptime.

{% stepper %}
{% step %}
<mark style="color:$success;">**The "Quick Wins" (High Risk, Zero/Low Disruption)**</mark>

These are critical security holes that the IT team or advisor can fix in the background. End-users will likely not even notice these changes.

**Examples:**&#x20;

* Changing the default factory password on the boundary firewall/router.
* Removing dormant or unused user accounts.
* Removing administrative privileges from standard users (assuming they don't actually need them for daily tasks).
* Turning on the software firewall on company laptops.

**Consulting approach:**

> _"We can do these immediately in the background. Your staff won't notice any downtime, but it instantly makes you much safer."_
{% endstep %}

{% step %}
<mark style="color:$warning;">**Scheduled Security Bumps (High Risk, Medium Disruption)**</mark>

These are critical fixes that _will_ require the user to change their behavior or take action. They cannot be done as a surprise.

**Examples:**

* Rolling out Multi-Factor Authentication (MFA) across Google Workspace/Microsoft 365.
* Enforcing a new password policy (forcing users to log out and create new passwords).
* Pushing a backlog of operating system updates that will force laptops to reboot.

**Consulting approach:**

> _"These are critical to stop hackers, but they will affect how your team logs in. We will schedule this for Friday afternoon, provide a simple 'How-To' guide for the staff, and I will be on standby to help anyone who gets locked out."_
{% endstep %}

{% step %}
<mark style="color:$danger;">**Strategic/Capital Expenditure (High Risk, High Disruption)**</mark>

These are fixes that require buying new equipment or migrating to new systems. They take time, budget, and planning.

**Examples:**&#x20;

* Replacing an End-of-Life (EOL) operating system.
* Moving away from an unsupported, legacy business application.

**Consulting approach:**

> _"We cannot fix this overnight because it requires buying a new laptop and migrating your files. Let's isolate that Windows 8.1 machine as much as possible right now, and set a target date next month for the hardware replacement so we can budget for it."_
{% endstep %}

{% step %}
<mark style="color:$primary;">**Policy & Cleanup (Low Risk, Low Disruption)**</mark>

These are technicalities required for CE compliance, but they aren't the most pressing immediate threats compared to the above.

**Examples:**

* Setting up auto-run blocks (autorun/autoplay) on USB drives.
* Uninstalling bloatware or unapproved applications that aren't actively malicious but violate the "approved software" control.

**Consulting approach:**

> _"Once the major risks are handled, we will quietly push these final configuration changes to ensure you pass the certification audit."_
{% endstep %}
{% endstepper %}

#### Golden Rules for Minimising Business Disruption

1. <mark style="color:$warning;">**Never "Surprise" the User:**</mark> Always communicate changes before they happen. Tell them _why_ it's happening using the "<mark style="color:$info;">So What?</mark>" framework ([ncsc-small-organisation-guide.md](advisor-resources/ncsc-small-organisation-guide.md "mention")).
2. <mark style="color:$warning;">**Batch the Reboots:**</mark> If you are installing antivirus, updating Windows, and applying a software patch, do them all in the same maintenance window so the user only has to reboot their machine once.
3. <mark style="color:$warning;">**Respect Peak Hours:**</mark> Schedule network downtime (like a router firmware update) for out-of-hours or their quietest operational period.
4. <mark style="color:$warning;">**Pilot Testing:**</mark> If implementing Application Allowlisting, test it on one IT/Admin device first to ensure it doesn't accidentally block core business software (like QuickBooks) before rolling it out to the whole office.

***

## Post-Remediation Validation

The remediation phase is not complete until the Advisor has proven the fixes actually work.&#x20;

{% hint style="info" %}
#### Verification

Adopt a "trust, but verify" mindset.
{% endhint %}

#### The Validation Process:

1. <mark style="color:$info;">**Re-Test Failed Controls:**</mark> Do not just accept an email from IT saying "the firewalls are on." Go back to the specific assets that failed and visually or technically verify that the host-based software firewall is now active and blocking inbound connections.
2. <mark style="color:$info;">**Verify Processes, Not Just Tech:**</mark> If the initial gap was a failure to remove accounts for ex-employees, ask IT to demonstrate their newly created offboarding process by showing that a recent leaver's account has actually been disabled.
3. <mark style="color:$info;">**Draft the Final Validation Report:**</mark> Produce a concise closing report for senior leadership. This document confirms that all previously identified gaps are successfully closed, the technical environment aligns with the CE standard, and the business is clear to formally apply for certification.

***

## The Closing Report

The closing report is a concise, executive-facing document. Its primary purpose is to officially confirm to the business leaders that the agreed remediation plan has been successfully executed, validated, and that their IT environment now meets the Cyber Essentials standard.

### Structure of the Closing Report

A high-quality closing report should contain the following four sections:

#### 1. Executive Summary

A short, plain-English statement confirming the overall status.

* <mark style="color:$info;">**Goal:**</mark> Tell the CEO immediately if they are ready to pass the assessment.
* <mark style="color:$info;">**Example**</mark>_<mark style="color:$info;">**:**</mark>_ "Following the successful implementation of the agreed remediation plan, I can confirm that \[Client Name]'s IT infrastructure now aligns with the technical requirements of the Cyber Essentials vx.x standard. The organisation is cleared to proceed with the formal self-assessment."

#### 2. Summary of Closed Gaps

A brief recap of the major vulnerabilities identified in the initial Gap Analysis and how they were resolved. This reminds the client of the value provided.

* <mark style="color:$info;">**Goal:**</mark> Map the fix to the original business risk.
* <mark style="color:$info;">**Example:**</mark> "The previously identified risk regarding unmanaged personal devices (BYOD) has been mitigated. Conditional Access policies are now active, restricting company data access strictly to company-owned, managed laptops."

#### 3. Validation Methodology (The "Proof")

This is where the Advisor demonstrates the "trust, but verify" behaviour required of a Cyber Advisor. Briefly explain _how_ it was proven the fixes were put in place, especially if an external MSP did the actual keyboard work.

* <mark style="color:$info;">**Goal:**</mark> Provide assurance that the IT environment wasn't just fixed on paper, but in reality.
* <mark style="color:$info;">**Example:**</mark> "Validation was conducted on \[Date]. I visually inspected a sample of three remote laptops to confirm the host-based software firewall was active. I also reviewed the Microsoft 365 admin logs to verify that Multi-Factor Authentication (MFA) is actively enforcing logins for all staff accounts."

{% hint style="warning" %}
#### "Scoped Out" Assets

If the business couldn't afford to fix a device (e.g., a legacy Windows 8 PC) and the agreed remediation was to isolate it from the network to remove it from scope, the closing report <mark style="color:$warning;">**MUST**</mark> explicitly state that this device is now out of scope and cannot be reconnected to the internet.
{% endhint %}

#### 4. Next Steps (Certification)

Clear instructions on what the business needs to do next to actually get their certificate.

* <mark style="color:$info;">**Goal:**</mark> Guide them through the final administrative hurdle.
* <mark style="color:$info;">**Example:**</mark> "You may now log into the IASME portal to complete your self-assessment questionnaire. Ensure you declare the scope exactly as we defined it in phase one (excluding home ISP routers). Once submitted, the external assessor will review your answers and award the certification."
