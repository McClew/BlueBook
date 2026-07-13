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

# WMI Subscriptions

Windows Management Instrumentation (WMI) allows administrators to automate tasks. Threat actors leverage it to create powerful, completely "fileless" persistence engines hidden inside complex system databases.

**Path:** `C:\Windows\System32\wbem\Repository\OBJECTS.DATA`

{% hint style="info" %}
#### Persistence Requirements

WMI persistence requires three structural components working in unison:&#x20;

* an `__EventFilter` (the trigger, like system uptime reaching 300 seconds),&#x20;
* an `__EventConsumer` (the payload action, typically an obfuscated CommandLine or ActiveScript block),&#x20;
* and a `__FilterToConsumerBinding` (the logical link joining them).

Because these definitions exist solely within the binary structures of the `OBJECTS.DATA` multi-purpose container database, standard host antivirus scanners frequently fail to detect them. We must process this archive using dedicated forensic parsers like `PyWMIPersistenceFinder` to extract compiled scripts or encoded Base64 execution strings.
{% endhint %}
