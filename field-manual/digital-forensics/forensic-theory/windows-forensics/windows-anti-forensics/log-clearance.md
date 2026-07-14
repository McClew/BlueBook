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

# Log Clearance

#### Event Log Clearance (Event ID 1102 & 104) <a href="#p-rc_fd4306d0ae724465-30" id="p-rc_fd4306d0ae724465-30"></a>

When adversaries compromise a host, they often clear the local event logs before exiting to destroy the records of their lateral movement, privilege escalation, or privilege abuse.

**Primary Target:** `C:\Windows\System32\Winevt\Logs\` database files.

***

## The Audit Log Was Cleared

When an administrator or attacker clears a Windows event log, the system immediately writes a new, singular event to mark the action:

`Security Log` - `Event ID 1102`: "The audit log was cleared." This event explicitly captures the Account Name and Logon ID of the user profile that initiated the clearance.

> #### #1102
>
> Event 1102 is logged whenever the Security log is cleared, REGARDLESS of the status of the Audit System Events audit policy. The Account Name and Domain Name fields identify the user who cleared the log.\
> \
> Logon ID allows you to correlate backwards to the logon event ([4624](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4624)) as well as with other events logged during the same logon session.

`System Log` - `Event ID 104`: Logged when any log channel _other_ than Security (such as Application or PowerShell) is cleared.

Because Windows event logs cannot be partially cleared via standard APIs a sudden, clean slate of logs starting with `Event ID 1102` outside of documented maintenance windows is an immediate high-severity incident indicator.
