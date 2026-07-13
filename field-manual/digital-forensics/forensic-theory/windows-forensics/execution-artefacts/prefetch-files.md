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

# Prefetch Files

The Prefetching mechanism monitors the first 10 seconds of an application's execution to cache the files it reads, accelerating future launches.

* Path: `C:\Windows\Prefetch`
* Forensic Value: Contains the application name, execution path hash, run counter, and up to 8 distinct execution timestamps (on Windows 8 through 11).

***

Prefetch file names append an 8-character cryptographic hash derived from the application's execution directory path (e.g., `CMD.EXE-AC1A44FA.pf`). If a threat actor copies a malicious version of `cmd.exe` to an obscure path, the resulting prefetch file will have a completely different hash string than the legitimate system binary, instantly flagging path masquerading.
