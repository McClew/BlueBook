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

# Risk Assessment

Risk Assessment is the comprehensive, structured, and defensible way to evaluate and prioritise risks. A standard assessment process involves a logical progression: characterising the system, identifying threats and vulnerabilities, analysing controls, and finally determining the risk score.

There are two primary analysis tools:

* **Qualitative Risk Analysis:** Evaluates risk based on subjective measures rather than objective financial data. It relies on human judgment, experience, and tools like a color-coded Risk Matrix. It is fast and excellent for initial triage.
* **Quantitative Risk Analysis:** Uses numerical values - specifically "dollars" and probabilities - to measure risk. It removes subjectivity and replaces it with hard data, historical trends, and financial modeling.

_See_ [risk-calculation.md](risk-calculation.md "mention") _for more information._

***

## Common Methodologies

Several established methodologies provide structured approaches to risk assessment.

### NIST SP 800-30

The primary risk management framework used by the US Federal Government. It focuses on identifying risks to federal information systems and determining appropriate security controls. It relies heavily on qualitative assessment but supports quantitative methods.

<mark style="color:$info;">**Focus & Key Differences:**</mark> This framework is highly structured, IT-centric, and heavily tied to the US Federal Government (FISMA compliance). It is part of the broader NIST Risk Management Framework (RMF) and is specifically designed to help organisations choose the right technical and operational security controls (often mapping to the NIST SP 800-53 catalog).

<mark style="color:$info;">**The Four-Step Lifecycle:**</mark>

1. **Prepare:** Define the scope, boundaries, and organisational context: "what are we assessing and why?".
2. **Conduct:** Identify threats and vulnerabilities, calculate likelihood and impact, and determine the final risk levels.
3. **Communicate:** Share the findings with decision-makers to guide budget and defense strategies.
4. **Maintain:** Continuously monitor risk factors and update the assessment as the technical environment changes.

<mark style="color:$info;">**Primary Deliverables:**</mark> A formal Risk Assessment Report (RAR) detailing threat-vulnerability pairs, calculated risk levels, and recommended security controls.

### OCTAVE (Operationally Critical Threat, Asset, & Vulnerability Evaluation)

Developed by the CERT Division at Carnegie Mellon University. This framework is heavily focused on organisational risk and strategic assessment rather than just IT systems. It is unique because it emphasises self-directed risk assessment by internal organisational teams rather than external consultants.

<mark style="color:$info;">**Focus & Key Differences:**</mark> Unlike NIST's heavy IT focus, OCTAVE views risk through a broader business and operational lens. It is unique because it is _**self-directed**_. **It is designed to be run by an internal, interdisciplinary team** (typically Management, Operations, and IT) rather than relying on external cybersecurity consultants. It empowers the people who know the business best to secure it.

<mark style="color:$info;">**OCTAVEs three distinct phases:**</mark>

1. **Build Asset-Based Threat Profiles:** Identify the organisation's critical assets (data, systems, people) and evaluate the threats against them from a business perspective.
2. **Identify Infrastructure Vulnerabilities:** Examine the specific IT components and networks that support those critical assets.
3. **Develop Security Strategy & Plans:** Conduct the risk analysis and decide on mitigation strategies.

<mark style="color:$info;">**Primary Deliverables:**</mark> A customised Protection Strategy and Mitigation Plan.

{% hint style="info" %}
#### Streamlined OCTAVE Variations

Traditional OCTAVE can be very documentation-heavy, which later led to the creation of streamlined versions like OCTAVE Allegro and OCTAVE-S for smaller businesses.
{% endhint %}

### ISO/IEC 27005

Part of the broader ISO 27000 series, this standard provides guidelines for information security risk management in support of an Information Security Management System (ISMS). It is highly customisable and focuses on continuous improvement.

<mark style="color:$info;">**Focus & Key Differences:**</mark> This is the international standard for information security risk management. Its primary goal is to support the creation and maintenance of an Information Security Management System (ISMS), specifically for ISO 27001 certification. Unlike NIST, it is highly flexible and does _not_ mandate a single rigid methodology; rather, it outlines the necessary components a good risk management process must have.

<mark style="color:$info;">**Loop of six key components:**</mark>

1. **Context Establishment:** Setting the internal and external criteria for how risks will be identified and calculated.
2. **Risk Assessment:** The actual identification, analysis, and evaluation of risks.
3. **Risk Treatment:** Deciding how to handle the risk (Avoid, Modify, Share, or Retain).
4. **Risk Acceptance:** Formally accepting risks that fall within the organisation's tolerance levels.
5. **Risk Communication & Consultation:** Sharing risk data and decisions with stakeholders.
6. **Risk Monitoring & Review:** Keeping the risk picture updated as threats evolve.

<mark style="color:$info;">**Primary Deliverables:**</mark> A Risk Treatment Plan and documented Risk Acceptance Criteria that prove to auditors the organisation is actively managing risk according to ISO standards.
