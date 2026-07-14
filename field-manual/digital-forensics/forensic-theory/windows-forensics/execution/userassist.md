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

UserAssist is an Explorer-centric tracking mechanism located inside the user's personal `NTUSER.DAT` registry hive. It is a vital asset when we need to prove attribution (i.e. _which_ specific user ran a program).

<figure><img src="../../../../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

UserAssist tracks applications launched through the native Windows Explorer shell environment. This includes items clicked via the Start Menu, shortcuts run from the desktop, or binaries launched through control panel applets.

{% hint style="warning" %}
## Explorer Tracking

User Assist relies on Explorer tracking, command-line execution or scripts running via CLI utilities (like `PowerShell` or `whoami`) will not generate entries here.\
\
If an attacker leverages lateral movement via an administrative command-line session (e.g. `psexec` or WinRM) without spawning a full Explorer shell GUI session, no UserAssist entries will be written.
{% endhint %}

The records are stored inside two main GUID subkeys under `HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist`:

* `{CEBFF5CD-ACE2-4F4F-9178-9926F41749EA}` – Tracks executable files.
* `{F4E57C4B-2036-45F0-A9AB-A7476DBDFA54}` – Tracks shortcut (`.lnk`) files.

***

## Obfuscation

UserAssist keys are obfuscated using a ROT13 cipher (e.g., `calc.exe` appears as `pelg.rkr`) to prevent basic system searches from corrupting the entries
