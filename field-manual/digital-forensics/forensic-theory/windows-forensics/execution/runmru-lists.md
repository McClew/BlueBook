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

# RunMRU Lists

The Run Most Recently Used (MRU) list is an explicit ledger of user-driven commands executed directly through the standard Windows Run dialogue box (`Win + R`).

Every time a user launches a tool or script using the Run dialogue, the entry is tracked natively within that specific user’s registry profile:

`HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\RunMRU`

Inside this key, individual commands are written to value names matching single letters (`a`, `b`, `c`, etc.). Crucially, the order of execution is not determined by the registry timestamps, but by a separate value named MRUList.

***

## Evidence of Tampering

The `MRUList` value contains a simple text string indicating the order of entry (e.g., `cfbad`). The first letter in the string is always the most recently executed item.

When a threat actor attempts anti-forensics by manually deleting a specific entry value (such as `b`), the string sequencing fails to align. If you spot a missing letter sequence in the `MRUList` string value or gaps in the alphabetized list, it is concrete proof of manual tampering or direct registry deletion.
