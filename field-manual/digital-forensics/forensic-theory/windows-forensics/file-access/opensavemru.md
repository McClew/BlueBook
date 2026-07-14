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

# OpenSaveMRU

Whenever a user opens or saves a file through a standard Windows dialogue box application wrapper, Windows records the event here, linking user actions directly to files introduced to or extracted from the operating system platform.

**Path:** `HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSavePIDlMRU`

***

## External Sources

The `OpenSavePIDlMRU` structure is complex because it records data using PIDLs (ItemID Lists) rather than simple text strings. These binary blobs capture not only the target file name but also the target volume type (e.g., local disk, network share, or external storage).

If an entry points to a path like `E:\Confidential_Data\`, it confirms the user interacted with an external asset, even if that device is missing from the scene.
