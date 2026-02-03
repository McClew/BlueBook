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

# Identifying Malicious Outlook Persistence

A common TTP in Business Email Compromise is the creation of inbox rules that move or delete incoming emails. This allows an attacker to communicate with external victims (e.g., changing BACS details) without the legitimate account owner seeing the replies.

***

## Forensic Investigation Steps

### 1. Identification of Persistence Rules

Run this command to find rules designed to bury evidence. Look specifically for rules moving mail to "Deleted Items", "Archive", or "RSS Subscriptions".

{% code title="Identify rules that delete or move messages to sensitive folders" %}
```powershell
Get-InboxRule -Mailbox "user@company.co.uk" | 
Where-Object {($_.DeleteMessage -eq $True) -or ($_.MoveToFolder -like "*Deleted*") -or ($_.MoveToFolder -like "*Archive*")} | 
Select-Object Name, Priority, Enabled, Description | 
Export-Csv -Path "C:\Forensics\Rules_Report_$($user).csv" -NoTypeInformation
```
{% endcode %}

{% hint style="info" %}
#### What to look for

Rules with names like ".", "z", or "Archive" that were not created by the user.
{% endhint %}

### 2. Detecting Shadow Forwarding

Attackers often set up mailbox-level forwarding to exfiltrate data in real-time. This command checks for SMTP forwarding addresses.

{% code title="" %}
```powershell
Get-Mailbox -Identity "user@company.co.uk" | 
Select-Object UserPrincipalName, ForwardingAddress, ForwardingSmtpAddress, DeliverToMailboxAndForward
```
{% endcode %}

{% hint style="info" %}
#### Forensic Note

If `DeliverToMailboxAndForward` is set to `$False`, the legitimate user will never see the emails; they go only to the attacker.
{% endhint %}
