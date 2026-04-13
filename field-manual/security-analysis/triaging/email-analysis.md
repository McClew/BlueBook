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
---

# Email Analysis

## Containment

Before analysing the email, ensure the threat is contained for the end-user.

* **Isolate the Message:** Move the email to a secure quarantine folder or a dedicated analysis mailbox.
* **Prevent Interaction:** Ensure the user has not clicked any links or downloaded attachments. If they have, initiate the Incident Response (IR) protocol for endpoint compromise immediately.
* **Header Preservation:** Always analyse the "Original Message" or the `.eml`/`.msg` file to preserve full header metadata.

***

## Header Analysis

Look for inconsistencies in the following fields:

<table><thead><tr><th width="306">Field</th><th>What to Look For</th></tr></thead><tbody><tr><td>From / Display Name</td><td>Look for "Display Name Spoofing" (e.g., "IT Support <code>scammer@gmail.com</code>").</td></tr><tr><td>Return-Path</td><td>Ensure the bounce-back address matches the sender's domain.</td></tr><tr><td>Authentication (SPF/DKIM/DMARC)</td><td>Check for <code>fail</code> or <code>softfail</code>. Attackers often use compromised legitimate domains to bypass these.</td></tr><tr><td>Received Lines</td><td>Trace the IP addresses. Does the originating server match the purported sender's location?</td></tr></tbody></table>

***

## Content Analysis

Analyse the content of the email (without rendering images if possible).

* **Urgency and Tone:** Look for "Business Email Compromise" (BEC) hallmarks: unusual requests for bank details, urgent "overdue" invoices, or threats of account suspension.
* **Hyperlink Deception:** Hover over links (do not click) to reveal the actual destination. Look for Typosquatting (e.g., `micros0ft.com` instead of `microsoft.com`) or the use of URL shorteners (`bit.ly`, `t.co`).
* **Hidden Elements:** Check for "Zero-font" attacks or hidden text designed to bypass automated spam filters.

***

## Attachment Analysis

* **File Extensions:** Be wary of double extensions (e.g., `Invoice.pdf.exe`) or uncommon archive formats (`.iso`, `.vhd`, `.7z`).
* **Hash Analysis:** Calculate the file hash (MD5/SHA256) and check it against VirusTotal or MalwareBazaar.
* **Dynamic Analysis:** Execute the file in a sandbox (e.g., Any.Run, Joe Sandbox) to observe network callbacks or registry changes.

{% hint style="danger" %}
#### Sandboxing

Only handle attachments within a hardened sandbox or a disconnected virtual machine (VM).
{% endhint %}

***

## Indicators of Comliance

Once an email is confirmed as malicious, extract the following indicators to pivot our investigation:

1. **Sender IP Addresses:** Block at the perimeter firewall/gateway.
2. **Malicious URLs:** Add to web proxy blocklists.
3. **Attachment Hashes:** Search the environment for other instances of this file.
4. **Subject Lines:** Use these to identify other recipients within the organisation.
