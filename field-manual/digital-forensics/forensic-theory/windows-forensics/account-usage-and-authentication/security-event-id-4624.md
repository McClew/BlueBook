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

# Security Event ID 4624

#### Event ID 4624 - Successful Logon

Event ID 4624 is generated whenever a log session is successfully established on the local host, regardless of whether it originated locally or across the network. The Event Log discloses the target account name, security identifier (SID), logon process engine, and source network address.

**Path:** `C:\Windows\System32\Winevt\Logs\Security.evtx`

> #### #4624
>
> **An account was successfully logged on**
>
> This is a highly valuable event since it documents each and every successful attempt to logon to the local computer regardless of logon type, location of the user or type of account. You can tie this event to logoff events [4634](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4634) and [4647](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4647) using Logon ID.

The key metric within a 4624 event is the Logon Type field:

* Logon `Type 2` indicates interactive console access (someone physically at the keyboard).
* Logon `Type 3` represents a network connection (mapping a drive, accessing an SMB share).
* Logon `Type 10` confirms an RDP connection.

{% hint style="info" %}
#### Common Lateral Movement

If we see a standard domain admin account logging in via Logon `Type 3` followed immediately by local execution artefacts, it is a textbook indicator of lateral movement.
{% endhint %}
