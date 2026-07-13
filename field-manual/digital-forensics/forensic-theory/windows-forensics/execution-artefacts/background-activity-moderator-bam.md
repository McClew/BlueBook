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

* Path: `HKLM\SYSTEM\CurrentControlSet\Services\bam\UserSettings\{SID}`
* Forensic Value: Maps the absolute execution path and a 64-bit Windows FILETIME execution timestamp directly to a specific user's Security Identifier (SID).

***

{% hint style="warning" %}
#### Limited Record Lifetime & Sources

Unlike heavier forensic logs, BAM records are not permanent. Inactive entries are automatically pruned after 7 days of inactivity.

Crucially, BAM completely ignores executables launched directly from network shares or removable storage devices (like USB thumb drives).
{% endhint %}

