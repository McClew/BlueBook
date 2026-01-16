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

# Authentication & Logon

## Logon Types

<table><thead><tr><th width="127">Logon Type</th><th>Description</th></tr></thead><tbody><tr><td>2</td><td>Interactive (logon at keyboard and screen of system)</td></tr><tr><td>3</td><td>Network (i.e. connection to shared folder on this computer from elsewhere on network)</td></tr><tr><td>4</td><td>Batch (i.e. scheduled task)</td></tr><tr><td>5</td><td>Service (Service startup)</td></tr><tr><td>7</td><td>Unlock (i.e. unnattended workstation with password protected screen saver)</td></tr><tr><td>8</td><td>NetworkCleartext (Logon with credentials sent in the clear text. Most often indicates a logon to IIS with "basic authentication") <a href="http://www.windowsitpro.com/Articles/Print.cfm?ArticleID=45214">See this article for more information.</a></td></tr><tr><td>9</td><td>NewCredentials such as with RunAs or mapping a network drive with alternate credentials.  This logon type does not seem to show up in any events.  If you want to track users attempting to logon with alternate credentials see <a href="http://www.ultimatewindowssecurity.com/wiki/SecurityLogEventID4648.ashx">4648</a>.  MS says "A caller cloned its current token and specified new credentials for outbound connections. The new logon session has the same local identity, but uses different credentials for other network connections."</td></tr><tr><td>10</td><td>RemoteInteractive (Terminal Services, Remote Desktop or Remote Assistance)</td></tr><tr><td>11</td><td>CachedInteractive (logon with cached domain credentials such as when logging on to a laptop when away from the network)</td></tr></tbody></table>

***

## 4624

**An account was successfully logged on**

This is a highly valuable event since it documents each and every successful attempt to logon to the local computer regardless of logon type, location of the user or type of account. You can tie this event to logoff events [4634](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4634) and [4647](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4647) using Logon ID.

***

## 4625

**An account failed to log on**

This is a useful event because it documents each and every failed attempt to logon to the local computer regardless of logon type, location of the user or type of account.

***

## 4648

**A logon was attempted using explicit credentials**

This is a useful event for tracking several different situations:

* A user connects to a server or runs a program locally using alternate credentials.  For instance a user maps a drive to a server but specifies a different user's credentials or opens a shortcut under RunAs by shift-control-right-clicking on the shortcut, selecting Run as..., and then filling in a different user's credentials in the dialog box that appears.  Or a user logs on to a web site using new specific credentials.  That is the case above in the example - Administrator was logged on to the local computer and then accessed a SharePoint server sp01.icemail.com as [rsmith@mtg.com](mailto:rsmith@mtg.com).
* This event is also logged when a process logs on as a different account such as when the Scheduled Tasks service starts a task as the specified user. Logged on user: specifies the original user account.
* With User Account Control enabled, an end user runs a program requiring admin authority.  You will get this event where the process information is consent.exe.  Unfortunately Subject does not identify the end user.

Unfortunately this event is also logged in situations where it doesn't seem necessary.  For instance logging on interactively to a member server (Win2008 RC1) with a domain account produces an instance of this event in addition to 2 instances of [4624](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4624).

***

## 4768

**A Kerberos authentication ticket (TGT) was requested**

This event is logged on domain controllers only and both success and failure instances of this event are logged.\
\
At the beginning of the day when a user sits down at his or her workstation and enters his domain username and password, the workstation contacts a local DC and requests a TGT. If the username and password are correct and the user account passes status and restriction checks, the DC grants the TGT and logs event ID 4768 (authentication ticket granted).  \
\
If the ticket request fails Windows will either log this event, 4768 or [4771](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4771) with failure as the type.\
\
The User field for this event (and all other events in the Audit account logon event category) doesn't help you determine who the user was; the field always reads N/A. Rather look at the Account Information: fields, which identify the user who logged on and the user account's DNS suffix. The User ID field provides the SID of the account. \
\
Windows logs other instances of event ID 4768 when a computer in the domain needs to authenticate to the DC typically when a workstation boots up or a server restarts. In these instances, you'll find a computer name in the User Name and fields. Computer generated kerberos events are always identifiable by the $ after the computer account's name.\
\
This event records that a Kerberos TGT was granted, actual access will not occur until a service ticket is granted, which is audited by Event [673](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=673). If the PATYPE is PKINIT, the logon was a smart card logon.

***

## 4769

**A Kerberos service ticket was requested**

Whereas event ID [4768](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4768) lets you track initial logons through the granting of TGTs, this lets you monitor the granting of service tickets. Service tickets are obtained whenever a user or computer accesses a server on the network. For example, when a user maps a drive to a file server, the resulting service ticket request generates event ID 4769 on the DC.
