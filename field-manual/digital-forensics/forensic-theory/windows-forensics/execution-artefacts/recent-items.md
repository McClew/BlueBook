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

# Recent Items

The Recent Items infrastructure acts as the underlying file system framework that feeds visual elements into the user environment, aggregating records of accessed resources.

The Recent Items folder (located at: `C:\Users\<User>\AppData\Roaming\Microsoft\Windows\Recent`) serves as the central physical repository for system-generated LNK files and shell items.

***

## Mapping Activity

When assessing user interaction via the Recent Items architecture, keep an eye out for nested folder configurations. Opening a folder creates a shortcut to that folder inside `Recent`. By analysing the creation dates of these directory shortcuts, you can track the exact progression of an adversary as they navigated and mapped out the target file system during an active data exfiltration event.
