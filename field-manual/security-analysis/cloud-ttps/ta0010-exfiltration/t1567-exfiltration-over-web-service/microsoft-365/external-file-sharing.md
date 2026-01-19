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

# External File Sharing

An attacker creates sharing links - Anonymous or Secure - for sensitive files and sends them to external email addresses.

## Indicators

### Atypical Link Type Usage

A user who historically only uses "People in your organization" links suddenly creates multiple "Anyone with the link" (Anonymous) or "Specific People" (External) links.

### Automated Link Creation

An attacker script creates a large number of sharing links in a very short burst (e.g., 50+ links in under 2 minutes).

### Sharing from Sensitive Repositories

Sharing links created for files within restricted SharePoint sites (e.g., Board of Directors, HR, M\&A Folders) that have no history of external collaboration.

### Sharing by Privileged Service Accounts

Service or non-human accounts suddenly generating user-facing sharing links.
