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

Shimcache is used by the OS to identify application compatibility issues. It maps out files that may require "shims" to run properly on newer kernel versions.

* Path: `HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache`
* Forensic Value: Identifies execution paths and file modification dates.

***

{% hint style="warning" %}
#### Data Retention

Shimcache data is kept natively in kernel memory and is only written down to the SYSTEM hive upon a clean system shutdown or reboot. If a machine crashes or suffers a sudden loss of power, recent Shimcache entries will be lost; you must parse it out of a volatile memory dump instead.
{% endhint %}
