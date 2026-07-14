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

# The SAM Hive

The Security Accounts Manager (SAM) is a database file that stores local user account credentials, group memberships, and tracking metrics. The SAM stores local user parameters including Relative Identifiers (RIDs), password expiration timelines, login counters, and historical timestamp data.

**Path:** `C:\Windows\System32\config\SAM`

Because the SAM hive is locked continuously by the Windows kernel while running, you must extract it from an offline image or harvest it using Volume Shadow Copies.

Parsing the hive provides a Login Count and a Last Login Timestamp for every local user. If a built-in default account that is normally deactivated (such as the default local Administrator account, RID 500) shows a high login count and a recent timestamp, it indicates local privilege escalation or an oversight in local account hardening.
