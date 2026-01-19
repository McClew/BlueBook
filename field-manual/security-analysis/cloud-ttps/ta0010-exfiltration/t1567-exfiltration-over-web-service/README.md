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
---

# T1567 - Exfiltration Over Web Service

## Mitre ATT\&CK

> Adversaries may use an existing, legitimate external Web service to exfiltrate data rather than their primary command and control channel. Popular Web services acting as an exfiltration mechanism may give a significant amount of cover due to the likelihood that hosts within a network are already communicating with them prior to compromise. Firewall rules may also already exist to permit traffic to these services.
>
> Web service providers also commonly use SSL/TLS encryption, giving adversaries an added level of protection.

{% embed url="https://attack.mitre.org/techniques/T1567/" %}
