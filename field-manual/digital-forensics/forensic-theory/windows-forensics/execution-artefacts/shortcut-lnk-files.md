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

# Shortcut (LNK) Files

Windows Shell Link files (`.lnk`) are binary structures that point to a local or remote target file. The OS creates them automatically to populate menus, but they also serve as independent forensic evidentiary artefacts.

When a user double-clicks a document, picture, or executable, a corresponding `.lnk` file is generated within the user's hidden profile path:

`C:\Users\<User>\AppData\Roaming\Microsoft\Windows\Recent`

LNK files do not just record paths; they capture the target file's size, system flags, and its full MACB (Modified, Accessed, Created, MFT-Modified) timestamp history.

***

## External Storage Execution

The true investigative value of a LNK file lies in its structural LinkInfo block. This block records the Volume Serial Number (VSN) of the drive where the target file was located, alongside the target host's hardware MAC Address and NetBIOS name.

If we locate a LNK file pointing to a malicious payload, we can extract the VSN to definitively prove whether that payload was launched from an external USB storage drive or a specific network share.
