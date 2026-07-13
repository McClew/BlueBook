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

# Amcache

Amcache is a registry hive created by Windows to track programs that have been installed or run on the machine, serving as a primary target during malware triage.

* Path: `C:\Windows\AppCompat\Programs\Amcache.hve`
* Forensic Value: Records application installation time, path, file compilation timestamps, and cryptographic hashes.

***

{% hint style="info" %}
#### Survivable Threat Intelligence

Amcache is an absolute goldmine because it records the SHA-1 file hash of the executable. Even if an attacker executes a malicious tool and subsequently deletes it from the disk, the Amcache hive usually preserves this hash, enabling you to run it against intelligence databases like VirusTotal.
{% endhint %}
