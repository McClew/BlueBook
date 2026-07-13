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

# UserAssist

This is a specific set of subkeys within the user's registry hive tracking software launched via the graphical user interface (GUI).

* Path: `HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist`
* Forensic Value: Tracks execution count and the exact timestamp of when the user last interacted with the GUI application.

***

{% hint style="warning" %}
## Explorer Tracking

User Assist relies on Explorer tracking, command-line execution or scripts running via CLI utilities (like `PowerShell` or `whoami`) will not generate entries here.
{% endhint %}

UserAssist value names are entirely obfuscated using a ROT13 cipher (e.g., `calc.exe` appears as `pelg.rkr`).
