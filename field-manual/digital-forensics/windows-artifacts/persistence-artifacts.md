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

# Persistence Artifacts

Persistence techniques exploit various system components, such as registry keys, startup processes, scheduled tasks, and services, enabling threat actors to withstand reboots and security measures while continuing to carry out their objectives undetected.

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

## Schtasks

Windows provides a feature allowing programs to schedule specific tasks. These tasks reside in `C:\Windows\System32\Tasks`, with each one saved as an XML file. This file details the creator, the task's timing or trigger, and the path to the command or program set to run. To scrutinise scheduled tasks, we should navigate to `C:\Windows\System32\Tasks` and examine the XML files' content.

***

## Services

`Services` in Windows are pivotal for maintaining processes on a system, enabling software components to operate in the background without user intervention. Threat actors often tamper with or craft rogue services to ensure persistence and retain unauthorised access. The registry location to keep an eye on is: `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services`.
