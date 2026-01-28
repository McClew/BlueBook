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

# Outlook Attachment Downloads

When a user opens an attachment directly from Outlook, Windows creates a copy of that file in a hidden subdirectory. This is a critical location to investigate during phishing analysis or data exfiltration cases, as files may persist here even if the original email was deleted.

`C:\Users[USER]\AppData\Local\Microsoft\Windows\INetCache\Content.Outlook\[RANDOM_STRING]`

***

## Analysis Steps

Here is an overview of the steps required:

{% stepper %}
{% step %}
#### Identify the Path

Query the `HKEY_CURRENT_USER\Software\Microsoft\Office[VERSION]\Outlook\Security` key to find the exact path.
{% endstep %}

{% step %}
#### Verify Timestamps

Compare the `CreationTime` of the file in this folder to the `Received` time of the suspect email.
{% endstep %}

{% step %}
#### Hash Extraction

Generate `SHA256` hashes of files in this directory to check against threat intelligence feeds.

Tools:

* [virustotal.md](../../../toolbox/tooling/threat-intelligence/virustotal.md "mention")
{% endstep %}

{% step %}
#### Cleanup Check

If the folder is empty but the Registry key exists, it may indicate the threat actor - or an automated script - cleared their temporary internet files to hide tracks.
{% endstep %}
{% endstepper %}

***

## Locating the Path via Registry

The random 8-character subdirectory name is stored in the Windows Registry. Instead of hunting through `INetCache`, we can query the following key to find the exact path for the current user:

Registry Key: `HKEY_CURRENT_USER\Software\Microsoft\Office\[VERSION]\Outlook\Security`

Value Name: `OutlookSecureTempFolder`

{% hint style="info" %}
#### Note

The \[VERSION] varies by Office install (e.g., `16.0` for Outlook 2016/2019/365, `15.0` for Outlook 2013).
{% endhint %}

***

## Quick Acquisition

We can use this script to instantly identify the directory and list any files currently residing in this temp directory:

```powershell
$Path = (Get-ItemProperty "HKCU:\Software\Microsoft\Office\*\Outlook\Security").OutlookSecureTempFolder
Get-ChildItem -Path $Path -Recurse | Select-Object Name, Length, LastWriteTime
```

***

## Forensic Significance

### Execution Evidence

If a user ran an executable or script directly from an email, the source path in logs (like Sysmon Event ID 1) will point to this folder.

### Persistence

Files remain in this folder until the number of files exceeds 99, at which point Outlook may overwrite them (or until manually cleared).

### Duplicate Handling

If a user opens a file named `Invoice.pdf` multiple times, Outlook will version them as `Invoice (2).pdf`, `Invoice (3).pdf`, etc. This helps track how many times a user interacted with a malicious file.
