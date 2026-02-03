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
---

# Business Email Compromise

Business Email Compromise (BEC) is a form of phishing attack where a theat actor impesonates colleagues, executives, suppliers or trusted partners via email into transfering funds or revealing sensitive data. BEC often involves convincing emails sent via spoofed email address or compromised accounts to bypass security filters.

Unlike standard phishing emails that are sent out indiscriminately to large numbers of email address, BEC attacks are usually cradted to specific individuals and can be harder to detect.

***

## Preparation

### User Awareness Training

Control Type: Administrative & Preventative

Conduct regular User Awarness Training to teach employees what to look for, guarding against emails that slip through email security filters.

### Phishing Simulations

Control Type: Administrative & Preventative

Alongside User Awarness Training, Phishing Simulations enable us to ensure that what employees are learning can be put into praxis and provides quantitive data to measure how well employees are performing in this preventative measure.

### Multi-Factor Authentication

Control Type: Technical & Preventative

Enforce multi-factor authentication (MFA) for all email accounts, this ensures that if user credentials are leaked, that the threat actor cannot immediately take advantage.

### Logging

Control Type: Technical & Detective

Ensure audit logging (e.g., Microsoft 365 Unified Audit Log) is enabled and retained for at least 90 days.

### Integrated Cloud Email Security (ICES)

Control Type: Technical & Preventative, Detective

Implement an ICES product to automatically filter suspicious emails from both within and without the clients domain. These tools can often provide:

* **Brand Impersonation Protection:** Configure the tool to monitor for "look-alike" domains (typosquatting) of the company and key UK suppliers.
* **User Coaching (In-line Banners):** Enable dynamic banners to provide real-time "point-of-failure" training to staff.
* **Automated Remediation:** Ensure the service has "Write" permissions to the mail tenant to allow for the automated clawback of malicious emails across all mailboxes once a threat is identified.

### Cloud Detection & Response (CDR)

Control Type: Technical & Preventative, Detective

A CDR solution can be integrated to monitor cloud solutions such as Microsoft 365. These product often provide:

* **Behavioural Baselines:** Establish "normal" user behaviour patterns (e.g., typical login times, IP ranges, and file access volumes) to reduce false positives.
* **Alert Correlation:** Configure logic to link disparate events, such as a "Successful MFA Bypass" followed immediately by "Global Admin Role Assignment."
* **Impossible Travel Policies:** Define geographical boundaries; any login from outside of the UK or sanctioned operating regions must trigger an automatic high-priority alert or account freeze.

***

## Detection & Analysis

### Indicators of Attack (IOA)

* **Email Security Alerts:** ICES flags "High-Risk" brand impersonation or "Look-alike" domain activity.
* **MFA Fatigue:** Multiple "Deny" logs on MFA requests followed by a "Success" (indicating the user was worn down).
* **Abnormal Logins:** CDR alerts for "Impossible Travel" or successful logins from non-UK IP addresses.
* **Anomalous Discovery:** Unexpected "Search" queries in Outlook/SharePoint for keywords like _Invoice, Payment, BACS,_ or _Payroll_.

### Indicators of Compromise (IOC)

* **Stealth Rules:** New inbox rules created to "Move to Deleted Items" or "Mark as Read" to hide attacker replies.
* **External Forwarding:** Unauthorised auto-forwarding rules sending mail to external domains.
* **Mailbox Purging:** Large volumes of items moved to the "Recoverable Items" folder or hard-deleted.
* **Delegation Changes:** Unauthorised granting of "Full Access" or "Send As" permissions on executive or finance mailboxes.
* **Legacy Auth:** Successful logins via legacy protocols (IMAP/POP3) which bypass modern MFA.

### Triage & Scope

1. **Identity Verification:** Compare the suspicious session IP against the user's known UK home/office locations.
2. **Breadth Check:** Use CDR to see if the same malicious IP has accessed other staff accounts.
3. **Data Impact:** Identify if the compromised account has "Global Admin" or "Privileged Role" status.

***

## Investigation

### Common Tactics, Techniques, and Procedures (TTPs)

#### "Silent Inbox" Technique

Threat actors create rules to move all incoming mail - or mail containing keywords like _invoice, payment, hack, spoof,_ or _phish -_ directly to the 'Deleted Items', 'Archive', or 'RSS Subscriptions' folders.

This allows them to hide their activity while continuing to utilise the compromised account for further attacks. See [t1564.008-email-hiding-rules](../field-manual/security-analysis/cloud-ttps/ta0005-defence-evasion/t1564-hide-artifacts/t1564.008-email-hiding-rules/ "mention").

#### "Mark as Read" Sweep

Rules configured to automatically mark all new mail as "Read," ensuring the victim does not receive "New Mail" notifications on their mobile or desktop.

#### Shadow Forwarding

Stealthy forwarding rules (often hidden via PowerShell) that send copies of all outbound/inbound mail to an external attacker-controlled address.

#### Conversation Thread Hijacking

The attacker monitors an existing thread (e.g., a BACS transfer discussion), then interjects from the compromised account with "updated" bank details, deleting the original sent message to hide the trail.

#### Folder Nesting

Moving critical correspondence into deeply nested subfolders (e.g., `Inbox > Drafts > Templates > [Hidden]`) to use the mailbox as a staging area for data exfiltration.

### Investigation Steps

#### Phase A: Scope & Persistence (Immediate)

1. Active Session Review: Check for concurrent logins from suspicious IPs.
2. Mailbox Rule Audit: Identify "Hide" or "Delete" rules immediately. This is the highest priority as it prevents the user from seeing your internal security alerts.
3. Forwarding & Delegation: Check for `ForwardingAddress` or `ForwardingSmtpAddress` settings and "Full Access" permissions granted to other mailboxes.

#### Phase B: Impact Assessment (Mid-Investigation)

4\. Sent Items Analysis: Review 'Sent Items' and 'Deleted Items' for fraudulent invoices or "lure" emails sent to external UK partners or internal Finance teams.

5\. Search History: Use the Unified Audit Log to see if the attacker searched for "BACS", "Invoice", "Payment", or "Urgent".&#x20;

6\. Data Exfiltration: Check for large downloads from SharePoint/OneDrive or mass-forwarding of attachments.

#### Phase C: Root Cause Analysis (Post-Containment)

7\. Auth Method Review: Identify the entry vector—was it a successful Phish, an MFA bypass (Session Hijacking), or an exploit of a Legacy Protocol (IMAP/POP3)?

8\. App Registrations: Check for malicious "OAuth" apps. Attackers often trick users into "Accepting Permissions" for a fake app, giving them permanent access without needing a password.

***

## Containment

### Session Revocation

Immediately terminate all active sessions to remove the threat actor.

### Rule Purge

Bulk-delete all rules identified during the investigation phase.

### BACS/Finance Freeze

Notify the Finance department to pause all pending payments associated with any thread the threat actor touched.

### Domain Blocking

Add any external domains found in forwarding rules to the organisation-wide blacklist.
