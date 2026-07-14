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

# MountedDevices key

The `MountedDevices` registry key maps persistent logical drive letters to their underlying physical volumes or hardware components. This regkey is essential for linking the unique serial number of the suspect USB drive to the active drive letter (e.g. `E:`, `F:`) assigned by the operating system.

**Registry Path:** `HKLM\SYSTEM\MountedDevices`

***

## Connecting the Serial to the Drive Letter

Within `MountedDevices`, we will find values starting with `\DosDevices\X:` (where `X` is the drive letter). The binary value data of these entries contains the unique serial number (or parent prefix ID) of the corresponding device.

By matching this data string to your `USBSTOR` serial database, we can confidently state:&#x20;

> _"The thumb drive with serial number `001D923F900B` was mounted under drive letter `E:`."_

This drive letter can then be used to cross-reference auto-generated LNK files or RecentDocs entries.
