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

# Startup Folders

The classic, lowest-barrier auto-start location where shortcuts or programs are stored to execute automatically when a user logs on.

* **User-specific:** `C:\Users\<User>\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\`
* **Global / All Users:** `C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup\`

While simple to deploy and clean up, putting a binary or `.lnk` structure here generates highly resilient metadata. Even if an adversary quickly removes a shortcut file from the Startup directory before you perform a system imaging acquisition, the record leaves undeniable metadata structures behind.

We can recover these traces by parsing the `$MFT` (Master File Table) record index anomalies or carving the parent directory's Slack Space to reconstruct the deleted entry's timestamps.
