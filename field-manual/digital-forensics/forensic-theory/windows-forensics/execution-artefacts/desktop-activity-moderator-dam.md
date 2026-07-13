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

* **Primary Path:** \
  `HKLM\SYSTEM\CurrentControlSet\Services\dam\UserSettings\{USER_SID}`
* **Alternative Active State Path:** \
  `HKLM\SYSTEM\CurrentControlSet\Services\dam\state\UserSettings\{USER_SID}`

Values within this key contain the absolute file path to the executed desktop application. The value data contains a binary blob holding a 64-bit Windows FILETIME timestamp in Coordinated Universal Time (UTC). The operating system updates this specific value data when the application is launched or when it is evaluated during a power-state transition.

***

## Forensic Gaps & Limitations

Just like BAM, relying solely on DAM will introduce blind spots to your timeline analysis if you don't know its inherent constraints:

* **Temporal Decay:** DAM logs are not a permanent record of past activity. Inactive entries or entries for executables that have since been removed from the file system are routinely purged by the OS after 7 days.
* **Removable Storage Bypass:** Applications executed directly from external media (such as USB thumb drives) or mounted network file shares are completely bypassed by the DAM driver to avoid disrupting peripheral power states.

{% hint style="warning" %}
#### Timestamp Drift

DAM execution timestamps can occasionally exhibit a drift or update delay of several minutes depending on when the system flushes its power management states to disk. You must never use DAM as a definitive standalone clock timestamp; always cross-reference it with the high-fidelity timestamps found in Prefetch files or UserAssist logs.
{% endhint %}
