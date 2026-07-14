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

Amcache is an independent registry hive that tracks applications, drivers, and setup installations. It is arguably one of the most powerful triage locations for discovering unknown malware or anti-forensics tools.

{% hint style="info" %}
#### Survivable Threat Intelligence

Amcache keeps tracking records even if an application was executed only once and subsequently wiped using an anti-forensics tool or secure-deletion utility. Because `Amcache.hve` is written to disk as an independent log file transaction, the registry keys persist even when the target executable no longer exists anywhere on the master file table (MFT).
{% endhint %}

**Path:** `C:\Windows\AppCompat\Programs\Amcache.hve`

It records application installation time, path, file compilation timestamps, and cryptographic hashes.

<figure><img src="../../../../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

Amcache acts as an upgrade to the older `RecentFileCache.bcf`. It is a fully-formed standalone registry structure written directly to disk.

* **The Cryptographic Hash:** Its most critical asset is the recording of file cryptographic hashes (specifically SHA-1).
* **Compilation Metadata:** It stores the PE (Portable Executable) compilation timestamp extracted directly from the file header, allowing you to identify time-stomping anomalies if the disk modification date does not match the compile date.
