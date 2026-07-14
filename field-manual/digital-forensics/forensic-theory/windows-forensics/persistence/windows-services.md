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

# Windows Services

Services run background processes without requiring an active user to log into an interactive graphical interface session. Services capture the startup operational mode (`Start` value), the binary configuration target (`ImagePath`), and the system account context used during launch.

* **Path:** `HKLM\SYSTEM\CurrentControlSet\Services\`

***

## Start DWORD

When auditing services, map out the `Start` DWORD configuration key. Values of `0` (Boot) `1` (System), or `2` (Automatic) indicate the service launches during early-stage boot sequences.

Malware often masquerades as a legitimate system utility by registering its payload as a service running via a host driver container (e.g. configuring `ImagePath` to launch a malicious payload hidden as a service DLL through `svchost.exe -k`).
