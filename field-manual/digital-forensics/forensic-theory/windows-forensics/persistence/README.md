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

# Persistence Artefacts

Persistence techniques exploit various system components, such as registry keys, startup processes, scheduled tasks, and services, enabling threat actors to withstand reboots and security measures while continuing to carry out their objectives undetected.

<table data-search="true"><thead><tr><th width="181">Artefact Name</th><th width="275">Location</th><th width="173">Execution Context</th><th width="113">Retained on Reboot?</th></tr></thead><tbody><tr><td><a data-mention href="run-and-runonce-reg-keys.md">run-and-runonce-reg-keys.md</a></td><td>HKLM &#x26; HKCU Software hives</td><td>User Logon</td><td>Yes</td></tr><tr><td><a data-mention href="scheduled-tasks.md">scheduled-tasks.md</a></td><td><code>C:\Windows\System32\Tasks</code> &#x26; Registry</td><td>Time / Event Triggered</td><td>Yes</td></tr><tr><td><a data-mention href="windows-services.md">windows-services.md</a></td><td><code>HKLM\SYSTEM\CurrentControlSet\Services</code></td><td>System Boot / Startup</td><td>Yes</td></tr><tr><td><a data-mention href="wmi-subscriptions.md">wmi-subscriptions.md</a></td><td><code>C:\Windows\System32\wbem\Repository</code></td><td>Arbitrary WMI Event Trigger</td><td>Yes</td></tr><tr><td><a data-mention href="startup-folders.md">startup-folders.md</a></td><td>User Profile &#x26; ProgramData Directories</td><td>User Logon</td><td>Yes</td></tr></tbody></table>

***

## Registry

The Windows `Registry` acts as a crucial database, storing critical system settings for the Windows OS. This encompasses configurations for devices, security, services, and even the storage of user account security configurations in the Security Accounts Manager (`SAM`).

Adversaries often target the Windows Registry for establishing persistence. Therefore, it's essential to routinely inspect Registry autorun keys.

Example of `Autorun` keys used for persistence:

* **`Run/RunOnce Keys`**
  * HKEY\_CURRENT\_USER\Software\Microsoft\Windows\CurrentVersion\Run
  * HKEY\_CURRENT\_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce
  * HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
  * HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce
  * HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\\
* **`Keys used by WinLogon Process`**
  * HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon
  * HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Shell
* **`Startup Keys`**
  * HKEY\_CURRENT\_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders
  * HKEY\_CURRENT\_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders
  * HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders
  * HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\User

***

## Services

`Services` in Windows are pivotal for maintaining processes on a system, enabling software components to operate in the background without user intervention. Threat actors often tamper with or craft rogue services to ensure persistence and retain unauthorised access. The registry location to keep an eye on is: `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services`.
