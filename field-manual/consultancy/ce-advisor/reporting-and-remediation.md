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

**The 4-Part Reporting Structure**

To ensure the report is actionable and provides real value to clients, structure every failed control using this logical flow:

1. **The Observation:**
   * State the facts clearly based on your discovery.
   * _Example:_ "Three members of the sales team are using personal, unmanaged mobile phones to access the company's Google Workspace."
2. **The Compliance Gap:**
   * State the specific Cyber Essentials requirement that was not met.
   * _Example:_ "Under Cyber Essentials, any device accessing company data must enforce a screen lock, run supported software, and restrict malicious apps. We currently cannot verify these controls on personal devices."
3. **The Business Risk:**
   * Translate the gap into a business threat using the [ncsc-small-organisation-guide.md](advisor-resources/ncsc-small-organisation-guide.md "mention") pillars.
   * _Example:_ "If a sales rep loses their phone, or if it gets infected by a malicious app, attackers could gain access to your company emails and client data, leading to a severe data breach."
4. **The Actionable Recommendation:**
   * Provide clear, cost-aware options for the leadership to choose from.
   * _Example:_ "Option A: We implement Conditional Access to block personal phones, forcing staff to only use work laptops. Option B: We require staff to enrol their personal phones into a lightweight Mobile Device Management (MDM) profile to enforce screen locks."

***

## Sympathetic Remediation Planning

Once leadership approves the recommendations, the Advisor must work with internal IT staff, an external Managed Service Provider (MSP), or the staff themselves to deploy the changes.

The Cyber Advisor standard mandates a Professional, Collaborative, and Non-Judgemental approach.

**Key Strategies for Sympathetic Planning:**

* **Understand Business Priorities:** Do not deploy disruptive changes during critical business operations. If MFA registration needs to be applied to for all users, do not schedule it on the day the finance team processes payroll. Propose a phased rollout.
* **Acknowledge IT Workloads:** If working with an MSP or internal IT, treat them as partners, not subjects of an audit. Agree on timelines that respect their existing SLA commitments.
* **Find Cost-Effective Paths:** If a business is running a legacy, unsupported Windows 10 machine to operate a vital, expensive piece of manufacturing hardware, do not simply tell them to "buy a new machine." Work with IT to sympathetically remove the machine from scope (e.g., by completely air-gapping it from the internet or placing it behind a strict internal firewall).

***

## Post-Remediation Validation

The remediation phase is not complete until the Advisor has proven the fixes actually work.&#x20;

{% hint style="info" %}
#### Verification

Adopt a "trust, but verify" mindset.
{% endhint %}

**The Validation Process:**

1. **Re-Test Failed Controls:** Do not just accept an email from IT saying "the firewalls are on." Go back to the specific assets that failed and visually or technically verify that the host-based software firewall is now active and blocking inbound connections.
2. **Verify Processes, Not Just Tech:** If the initial gap was a failure to remove accounts for ex-employees, ask IT to demonstrate their newly created offboarding process by showing that a recent leaver's account has actually been disabled.
3. **Draft the Final Validation Report:** Produce a concise closing report for senior leadership. This document confirms that all previously identified gaps are successfully closed, the technical environment aligns with the CE standard, and the business is clear to formally apply for certification.

***

## The Closing Report

The closing report is a concise, executive-facing document. Its primary purpose is to officially confirm to the business leaders that the agreed remediation plan has been successfully executed, validated, and that their IT environment now meets the Cyber Essentials standard.

### Structure of the Closing Report

A high-quality closing report should contain the following four sections:

#### 1. Executive Summary

A short, plain-English statement confirming the overall status.

* **Goal:** Tell the CEO immediately if they are ready to pass the assessment.
* **Example**_**:**_ "Following the successful implementation of the agreed remediation plan, I can confirm that \[Client Name]'s IT infrastructure now aligns with the technical requirements of the Cyber Essentials vx.x standard. The organisation is cleared to proceed with the formal self-assessment."

#### 2. Summary of Closed Gaps

A brief recap of the major vulnerabilities identified in the initial Gap Analysis and how they were resolved. This reminds the client of the value provided.

* **Goal:** Map the fix to the original business risk.
* **Example:** "The previously identified risk regarding unmanaged personal devices (BYOD) has been mitigated. Conditional Access policies are now active, restricting company data access strictly to company-owned, managed laptops."

#### 3. Validation Methodology (The "Proof")

This is where the Advisor demonstrates the "trust, but verify" behaviour required of a Cyber Advisor. Briefly explain _how_ it was proven the fixes were put in place, especially if an external MSP did the actual keyboard work.

* **Goal:** Provide assurance that the IT environment wasn't just fixed on paper, but in reality.
* **Example:** "Validation was conducted on \[Date]. I visually inspected a sample of three remote laptops to confirm the host-based software firewall was active. I also reviewed the Microsoft 365 admin logs to verify that Multi-Factor Authentication (MFA) is actively enforcing logins for all staff accounts."

{% hint style="warning" %}
#### "Scoped Out" Assets

If the business couldn't afford to fix a device (e.g., a legacy Windows 8 PC) and the agreed remediation was to isolate it from the network to remove it from scope, the closing report **MUST** explicitly state that this device is now out of scope and cannot be reconnected to the internet.
{% endhint %}

#### 4. Next Steps (Certification)

Clear instructions on what the business needs to do next to actually get their certificate.

* **Goal:** Guide them through the final administrative hurdle.
* **Example:** "You may now log into the IASME portal to complete your self-assessment questionnaire. Ensure you declare the scope exactly as we defined it in phase one (excluding home ISP routers). Once submitted, the external assessor will review your answers and award the certification."
