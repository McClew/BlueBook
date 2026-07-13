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

The Windows Prefetching mechanism is designed to optimise system performance by mapping out the files and dependencies an application loads within its first 10 seconds of lifecycle activity.

**Path:** `C:\Windows\Prefetch`

Prefetch files contain the application name, execution path hash, run counter, and up to 8 distinct execution timestamps (on Windows 8 through 11).

***

## Architectural Breakdown

When an executable launches, the Cache Manager monitors its page faults and creates a corresponding `.pf` file.

* **The Path Hash Principle:** Prefetch filenames are formatted as `EXECUTABLE.EXE-[8-CHARACTER HASH].pf`. This hash is derived via a specific hashing algorithm based on the path from which the executable ran. For host processes like `svchost.exe` or `dllhost.exe`, the hash also incorporates command-line arguments to separate distinct service instances.
* **Timestamp Limits:** On Windows 7, only a single execution timestamp is recorded. On Windows 8 through 11, the file structure maintains an array of the last 8 execution timestamps alongside a continuous execution counter.

***

## Parsing Prefetch

Modern versions of Windows (Windows 10 and 11) store Prefetch files with standard MAM compression. The files start with the magic signature `MAM` in the file header rather than the traditional version bytes.

These raw files cannot be parsed using legacy hexadecimal tools; they must be decompressed or parsed using native Windows API functions or dedicated utilities like [eric-zimmermans-ez-tools.md](../../../../../toolbox/tooling/digital-forensics/eric-zimmermans-ez-tools.md "mention")'s: `PECmd`.
