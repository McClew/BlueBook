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

# Volume Shadow Copy (VSS) Deletion

Volume Shadow Copies are backup snapshots of the filesystem state. Attackers (especially ransomware groups) will destroy these snapshots to prevent system recovery and lock down their control over the machine.

***

## Tracking Shadow Wiping

Attackers routinely execute commands such as `vssadmin.exe delete shadows /all /quiet` or use PowerShell to invoke WMI commands targeting the `Win32_ShadowCopy` class.

While this successfully deletes the local recovery points, the execution of these commands is permanently recorded in `Security Event ID 4688` (Process Creation) and `Sysmon Event ID 1`, capturing the exact administrative session used.

Additionally, the sudden loss of VSS files can be spotted during forensic imaging when comparing physical disk boundaries against the MFT records.
