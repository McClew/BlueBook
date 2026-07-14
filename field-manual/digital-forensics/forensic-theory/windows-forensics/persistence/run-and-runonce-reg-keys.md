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

# Run & RunOnce Reg Keys

The most common and easily accessible auto-start execution points (ASEPs) within the Windows Registry ecosystem.

* **Machine-wide:** `HKLM\Software\Microsoft\Windows\CurrentVersion\Run` (and `RunOnce`)
* **User-specific:** `HKCU\Software\Microsoft\Windows\CurrentVersion\Run` (and `RunOnce`)

These keys contain value names pointing directly to binary command lines executed upon user authentication.

***

## Run vs RunOnce

The operational distinction between `Run` and `RunOnce` keys is structural. Keys in the `Run` subkey execute every single time the shell logs on. In contrast, entries inside `RunOnce` are automatically purged by the operating system kernel immediately after a single successful launch.

If we identify a payload path inside a `RunOnce` key via offline hive analysis, it implies the system was compromised but has not yet been restarted, or the persistence mechanism is designed to cycle itself dynamically.
