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

# LNK Files & Recent Items

System-generated link files function fluidly as both execution indicators and clear records of target document interaction, containing MAC(b) metadata timelines of the target file, volume parameters, and target physical device identifiers.

**Path:** `C:\Users\<User>\AppData\Roaming\Microsoft\Windows\Recent\`

***

## Network Shares

When a user opens a file, Windows automatically creates a `.lnk` file in the `Recent` directory. If the target file resides on a network share, the LNK file stores the network path (UNC path) and server share name. This provides immediate visibility into lateral file access across an enterprise environment directly from an offline workstation image.
