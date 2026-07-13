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

# Shimcache

The Application Compatibility Cache, or Shimcache, is a kernel-level mechanism used to identify backwards-compatibility issues with older applications running on modern Windows kernels. It maps out files that may require "shims" to run properly on newer kernel versions.

Unlike Prefetch or UserAssist, the primary purpose of Shimcache is not to track _execution history_, but to keep an inventory of binaries residing on the file system to determine if a shim patch is required.

**Registry Location:** `HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache`

{% hint style="warning" %}
#### Data Retention

Shimcache data is kept natively in kernel memory and is only written down to the SYSTEM hive upon a clean system shutdown or reboot. If a machine crashes or suffers a sudden loss of power, recent Shimcache entries will be lost; you must parse it out of a volatile memory dump instead.
{% endhint %}

***

## Confirming Execution

Shimcache populates entries for executables simply by them being browsed via a file dialogue or present on disk during system operations. To confirm execution, we must look at the internal execution flag.

In Windows 7, this was a distinct binary bit flag; in Windows 10 and 11, the structure was modified so that an entry's presence within the cache combined with other registry markers is indicative of system interaction, but does not definitively guarantee the binary successfully executed to completion.
