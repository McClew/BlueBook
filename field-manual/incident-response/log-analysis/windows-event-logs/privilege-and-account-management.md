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

# Privilege & Account Management

## 4672

**Special privileges assigned to new logon**

This event lets you know whenever an account assigned any "administrator equivalent" user rights logs on.  For instance you will see event 4672 in close proximity to logon events ([4624](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4624)) for administrators since administrators have most of these admin-equivalent rights.&#x20;

So, this is a useful right to detecting any "super user" account logons.  Of course this right is logged for any server or applications accounts logging on as a batch job (scheduled task) or system service.  See Logon Type: on event ID [4624](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4624).  You can correlate 4672 to [4624](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4624) by Logon ID:.

Note: "User rights" and "privileges" are synonymous terms used interchangeably in Windows.

Admin-equivalent rights are powerful authorities that allow you to circumvent other security controls in Windows.  Most admin equivalent privileges are intended for services and applications that interact closely with the operating system.  With just a few exceptions, most admin equivalent privileges neither need nor should be granted to human user accounts.

Some Microsoft documentation puts this in the "Sensitive Privilege Use / Non-Sensitive Privilege Use" subcategory. However our testing finds this in the "Special Logon" Category.

***

## 4720

**A user account was created**

Attributes show some of the properties that were set at the time the account was created. Notice account is initially disabled.

This event is logged both for local SAM accounts and domain accounts.

You will see a series of other User Account Management events after this event as the remaining properties are punched down, password set and account finally enabled.

***

## 4726

**A user account was deleted**

This event is logged both for local SAM accounts and domain accounts.\
\
You will also see event ID [4738](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4738) informing you of the same information.

***

## 4732

**A member was added to a security-enabled local group**

Active Directory

In Active Directory Users and Computers "Security Enabled" groups are simply referred to as Security groups. AD has 2 types of groups: Security and Distribution. Distribution (security disabled) groups are for distribution lists in Exchange and cannot be assigned permissions or rights. Security (security enabled) groups can be used for permissions, rights and as distribution lists. A domain local group means the group can only be granted access to objects within its domain but can have members from any trusted domain.

Local SAM

All groups are security groups in the computer's SAM. Local SAM groups can be granted access to objects on the local computer only but may have members from the local SAM and any trusted domain.
