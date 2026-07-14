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

# ShellBags

ShellBags are a set of registry keys that store user preferences for folder viewing options within Windows Explorer (such as icon size, sorting order, and window position). This maps out folder paths, creation dates, access dates, and modification dates of directories browsed by the user.

* &#x20;`HKCU\Software\Classes\Local Settings\Software\Microsoft\Windows\Shell\BagMRU`
* `HKCU\Software\Classes\Local Settings\Software\Microsoft\Windows\Shell\Bags`

**Note:** In offline analysis, these are primarily located within the user's `UsrClass.dat` hive, though some legacy configurations point to `NTUSER.DAT`.

{% hint style="info" %}
#### Anti-Forensic Resilience

ShellBags are exceptionally resilient against anti-forensic deletion. When a folder is deleted from the hard drive, its physical record is removed from the file system structure, but the corresponding entry within the `BagMRU` hierarchy remains completely intact.

This allows an investigator to reconstruct the exact name and path layout of a deleted directory tree, proving that the user not only had the folder on their machine but actively navigated inside it.
{% endhint %}
