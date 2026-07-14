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

# Threat Execution Hijacking

Advanced threat actors know that clearing logs via `Event ID 1102` alerts security teams immediately. To bypass this, they utilise memory-injection tools to suspend the active threads of the `EventLog` service process without terminating the process itself, this is called Threat Execution Hijacking.

**Primary Target:** Active system memory (specifically `svchost.exe` running the `EventLog` service).

***

## Detecting Suspended Logging Threads

Windows Event Logs write events sequentially, assigning a strict, incrementing Record ID integer to every new entry. If an attacker injects code to suspend the event log service threads, performs their malicious actions, and then resumes the threads, the physical files on disk will not show any "Log Cleared" events.

However, when we plot the timestamps of the Event IDs sequentially, we will identify a temporal black hole: a massive time jump during which no logs were generated, despite other forensic host indicators (like Prefetch, USN Journal, or Shimcache) proving that intensive file and network activity was occurring.
