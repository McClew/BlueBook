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

# Security Event ID 4625

#### Event ID 4625 Failed Logon

Event ID 4625 tracks every failed authentication attempt, offering immediate visibility into brute-force attacks or credential stuffing. It documents the exact username targeted, the authentication package used, and structural failure codes.

**Path:** `C:\Windows\System32\Winevt\Logs\Security.evtx`

> #### #4625
>
> **An account failed to log on**
>
> This is a useful event because it documents each and every failed attempt to logon to the local computer regardless of logon type, location of the user or type of account.

Do not just look at the event count; parse the Sub-Status Code inside the hexadecimal format. For instance:

* A sub-status code of `0xC000006A` means the username was correct but the password was wrong.
* A code of `0xC0000064` indicates the user account itself does not exist.

If the timeline shows thousands of `0xC0000064` errors followed by a sudden string of `0xC000006A` errors, the attacker transitioned from guessing user accounts to actively enumerating valid passwords.
