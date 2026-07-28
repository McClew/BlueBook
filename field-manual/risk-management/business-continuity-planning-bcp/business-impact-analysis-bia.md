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

# Business Impact Analysis (BIA)

The BIA does not care _how_ a system goes down (fire, ransomware, hardware failure). It only cares about what happens to the business when it is down.

The primary deliverables of a BIA are:

* A prioritised list of critical business functions.
* The financial and operational impact of losing those functions over time.
* The required resource dependencies to bring them back online.
* Strict timeframes for recovery.

***

## Key Metrics

<table><thead><tr><th width="94.3184814453125">Metric</th><th width="263.550537109375">Name</th><th>What it Measures</th></tr></thead><tbody><tr><td>MTD</td><td>Maximum Tolerable Downtime</td><td>The absolute maximum amount of time a business process can be down before the organisation suffers catastrophic, unrecoverable damage.</td></tr><tr><td>RTO</td><td>Recovery Time Objective</td><td>The target time set for the IT team to recover the physical systems, servers, and network infrastructure after a disaster.</td></tr><tr><td>WRT</td><td>Work Recovery Time</td><td>The time required to configure the recovered systems, restore data, test operations, and get business users actually working again.</td></tr><tr><td>RPO</td><td>Recovery Point Objective</td><td>The maximum acceptable amount of data loss, measured in time (e.g., "we can only afford to lose 4 hours of data"). This directly dictates your backup frequency.</td></tr></tbody></table>
