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

# Partition Diagnostics Logs

While registry keys show persistent configurations, Windows Event Logs record real-time hardware connection and configuration events as they happen

**Primary Path:** `C:\Windows\System32\Winevt\Logs\`

**Critical Event IDs for USB Lifecycle Auditing:**

`Microsoft-Windows-Partition/Diagnostic.evtx` - `Event ID 1006`: Triggers whenever a physical disk volume is parsed by the kernel. This event cannot be bypassed by standard user-level commands and is created during both device insertion and removal.

`Microsoft-Windows-Storage-ClassPnP/Operational.evtx` - `Event ID 507`: Logs the loading of the system's class driver framework, representing the physical arrival of the mass storage interface.

***

## Harvesting Serial Numbers from XML Blocks

The "friendly view" of Partition `Event ID 1006` often contains a generic string like _"For internal use only."_ However, if we pivot to the raw XML view of the log entry, the complete volume layout, hardware vendor metadata, and the raw device serial number are preserved within the `<EventData>` blocks. Because this event log rotates based on file size constraints, it is a key target for extracting high-fidelity connection histories that may have been cleared from other areas.
