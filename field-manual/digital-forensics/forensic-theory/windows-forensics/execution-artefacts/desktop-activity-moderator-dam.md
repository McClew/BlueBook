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

# Desktop Activity Moderator (DAM)

The Desktop Activity Moderator (DAM) is a kernel component introduced alongside [background-activity-moderator-bam.md](background-activity-moderator-bam.md "mention") in Windows 10. Its operational purpose is to regulate the resource and power consumption of desktop (Win32) applications specifically when a device enters a "Modern Standby" or "Connected Standby" state - a power profile where the screen turns off but the system remains connected to the network.

For investigators, DAM provides an identical telemetry format to BAM (capturing full paths and execution times tied to specific users), but its presence is highly dependent on the system's underlying physical architecture.

***

## Registry Location and Schema

DAM populates keys directly inside the SYSTEM registry hive, structure-mapped by the Security Identifier (SID) of the executing user account.

* Primary Path: `HKLM\SYSTEM\CurrentControlSet\Services\dam\UserSettings\{USER_SID}`
* Alternative Active State Path: `HKLM\SYSTEM\CurrentControlSet\Services\dam\state\UserSettings\{USER_SID}`

Values within this key contain the absolute file path to the executed desktop application. The value data contains a binary blob holding a 64-bit Windows FILETIME timestamp in Coordinated Universal Time (UTC). The operating system updates this specific value data when the application is launched or when it is evaluated during a power-state transition.
