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



***

## 4726



***

## 4732

