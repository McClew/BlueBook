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

# Background Activity Moderator (BAM)

BAM is a modern Windows service that manages the power consumption of desktop and background applications.

***

## Registry Location and Schema

BAM populates keys directly inside the SYSTEM registry hive, structure-mapped by the Security Identifier (SID) of the executing user account.

* **Primary Path:** \
  `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\bam\State\UserSettings{SID}`
* **Alternative Active State Path:** \
  `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\bam\UserSettings{SID}`

***

## Forensic Gaps & Limitations

Just like [desktop-activity-moderator-dam.md](desktop-activity-moderator-dam.md "mention"), relying solely on BAM will introduce blind spots to your timeline analysis if you don't know its inherent constraints:

* **Temporal Decay:** BAM logs are not a permanent record of past activity. Inactive entries or entries for executables that have since been removed from the file system are routinely purged by the OS after 7 days.
* **Removable Storage Bypass:** Applications executed directly from external media (such as USB thumb drives) or mounted network file shares are completely bypassed by the BAM driver to avoid disrupting peripheral power states.
