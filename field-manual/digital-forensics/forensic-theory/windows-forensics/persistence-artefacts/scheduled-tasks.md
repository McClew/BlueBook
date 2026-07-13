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

# Scheduled Tasks

Windows provides a feature allowing programs to schedule specific tasks. These tasks reside in `C:\Windows\System32\Tasks`, with each one saved as an XML file. This file details the creator, the task's timing or trigger, and the path to the command or program set to run.

To scrutinise scheduled tasks, we should navigate to `C:\Windows\System32\Tasks` and examine the XML files' content.

* _Disk files:_ `C:\Windows\System32\Tasks\`
* _Registry Index:_ `HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Schedule\TaskCache\`

{% hint style="info" %}
#### Evasion Techniques

Advanced adversaries often employ evasion techniques, they create a scheduled task and then delete its corresponding XML definition descriptor file from `C:\Windows\System32\Tasks` while leaving the internal binary keys active within the registry `TaskCache\Tasks` subkeys.

When cross-referencing our triage data, any missing mapping alignment between the physical file system directory and the `TaskCache` registry hive indicates an intentional defense evasion attempt.
{% endhint %}

