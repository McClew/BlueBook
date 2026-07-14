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

# SetupAPI Device Log

The `setupapi.dev.log` file is a plain text log maintained by the Windows PnP subsystem to document driver staging, installation, and update events. It acts as an independent audit trail detailing exactly when a specific USB devices' drivers were installed on the host machine for the very first time.

**Path:** `C:\Windows\INF\setupapi.dev.log`

***

## Time Zone Configuration

Unlike the registry and event logs, which natively default to UTC, timestamps within `setupapi.dev.log` are written in the system's Local Time at the moment the action took place.

When parsing this text file, we must search for the device's unique serial number, find the relevant `Section Start` header, and explicitly document this time relative to the target computer's configured Active Time Bias (time zone offset) before building our forensic timeline.
