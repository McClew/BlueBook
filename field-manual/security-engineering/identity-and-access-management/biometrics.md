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

# Biometrics



***

## Biometric Authentication Errors

Biometric authentication systems produce two types of errors that must be managed:

<mark style="color:red;">**Type 1 Errors:**</mark> <mark style="color:$info;">False Rejection Rate (FRR)</mark>, occurs when legitimate users are incorrectly denied access.

<mark style="color:$warning;">**Type 2 Errors:**</mark> <mark style="color:$info;">False Acceptance Rate (FAR)</mark>, occurs when unauthorised users are incorrectly granted access, with FAR representing the most serious security risk.

Organisations must balance these error rates based on their security requirements and operational tolerance, as lowering one typically increases the other.

### Biometric System Accuracy

Like all measurement systems, biometric systems are not perfect and produce two distinct types of errors that security professionals must understand and manage. These errors directly impact both security effectiveness and user experience, making them essential metrics for evaluating biometric implementations.

Organisations must carefully balance FAR and FRR, as lowering one typically increases the other. The acceptance balance depends on the security requirements of the protected assets and the tolerance for operational disruption.

### Type 1 Error: FRR

A Type 1 error occurs when the biometric system rejects a legimate user - someone whose biometric data matches the stored template but the system fails to recognise them. This is called a False Rejection Rate (FRR).

False rejections happen due to various factors including poor image quality, changes in appearance, environmental conditions, or variations in how the user presents their biometric.

The impact of high FRR is primarily operational and user-focused. Legitimate users become frustrated when repeatedly denied access leading to workarounds, reduced adoption of the biometric system or users circumventing security controls entirely.

From a business perspective, false rejections create support costs and reduce productivity as users must retry authentication or use alternative verification methods.

### Type 2 Error: FAR

A Type 2 error occurs when the biometric system accepts an unauthorised user - someone whose biometric data does not match the stored template but the system incorrectly grants them access. This is called the False Acceptance Rate (FAR).

False acceptances represent the more serious security risk, as they directly compromise the authentication mechanism's ability to prevent unauthorised access.

High FAR values indicate that the biometric system's matching threshold is too lenient, allowing imposters to gain access. This creates direct security vulnerabilities and potential complaince violations.&#x20;
