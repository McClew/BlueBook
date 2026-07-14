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

# MountPoints2 key

The `MountPoints2` key is stored inside the user-specific `NTUSER.DAT` registry hive. It tracks the volume mappings created during an individual user's active session. It provides the key evidence required for user attribution.

**Registry Path:** `HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\MountPoints2`

***

## Proving Who Logged On&#x20;

When a machine is shared by multiple employees, proving a USB drive was plugged in is not enough; you must prove _who_ did it. Because `MountPoints2` is nested within `NTUSER.DAT`, its keys are isolated to the specific user profile.

Finding the suspect USB's unique volume GUID or hardware serial number in this key is a reliable way to prove that specific user account was logged in, active, and mounting the external storage media.
