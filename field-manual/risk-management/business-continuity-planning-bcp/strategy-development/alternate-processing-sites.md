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
  anchors:
    visible: true
---

# Alternate Processing Sites

Alternative processing sites are critical components of any comprehensive business continuity and disaster recovery (BC/DR) strategy. These facilities provide workspaces, connectivity and other essnetial services that enabled an organisation to restore continuity capabilities and resume core business activities followign a disruption or disaster.

Organsiations can employ a mix of off-premise, on-premise, cloud-hosted or work-from-home capabilities depending on their specific needs and risk tolerance.

The selection of an appropriate alternate processing site directly impacts both the organisations recovery capabilities and its dinancial investment in BC/DR planning. Different types of sites offer varying levels of readiness, cost structures and recovery timeframes. Understanding these distinctions is essential to ensure that whatever recvovery option is chosen maintains the full spectrum of [<mark style="color:$info;">CIANA+PS</mark>](#user-content-fn-1)[^1] security requirements throughout the recovery process.

***

## Role in the Recovery Strategy

When a disruption occurs, the organisations ability to quickly restore operations depends heavily on the type of alternate processing site that has been established. These sites server as backup locations where teams can continue critical business functions, restore data from backups and archives and maintain communications with stakeholders.

The security of these alternate sites is paramount - recovery of capabilities and bringing the organisation back from disaster cannot be done if people cannot trust the data they're using or the communications and collaboration arrangements they rely on.

Alternate processing sites must be integrated into the overall BC/DR plan alongside backup and archival strategies. The organisation must consider not only the technical infrastructure at these sites but also the security controls, access management, and data protection measures that will be in place during recovery operations.

This includes ensuring that crytographic assets, digital certificates, and encryption keys necessary to access backed-up data are also available at the recovery site.

***

## Considerations for Site Selection

Organisation smust evaluate several factors when selecting an appropriate alternate processing site. These include:

<mark style="color:$primary;">**Recovery Time Objective (RTO):**</mark> How quickly systems must be restored.

<mark style="color:$primary;">**Revoery Point Objective (RPO):**</mark> How much data loss is acceptable.

{% hint style="info" %}
#### Key Metrics

See the [business-impact-analysis-bia.md](../business-impact-analysis-bia.md "mention")page's "Key Metrics" section for more information.
{% endhint %}

Additionally, organisations must consider their budget constraints, the criticality of different business functions and the types of disruptions they are most likely to face. Larger enterprises typically employ multiple types of alternate processing sites to address different recovery scenarios, while smaller organisations may need to priortise cost-effectiveness over rapid recovery capabilities.

[^1]: CIANA+PS is an expanded cyber security and information assurance framework that builds upon the traditional CIA triad by adding two core security pillars and a privacy/safety element.
