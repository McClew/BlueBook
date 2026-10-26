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

# Trusted Computing Base

Trusted Computing Base (TCB) is the minimal, core set of hardware and operating system functions and features that provide a highly reliable, secure and protected foundation for everything else. The TCB is the part of the system that keeps user mode programs from successfully attaining a privileged user status, which would grant them the power to directly manipulate hardware devices.

It is the lowest level enforcer of access control policies, which it enforces by establishing and preserving the seperation or memory and CPU resources in use by one process thread from being read, modified, or called into execution by another process.

The TCB also creates and controls the use of trusted paths that can exist between user-mode processes and each other or with hardware devices by means of their device drivers and service handlers. This seperation of process resources and the management of trusted paths are fundamental to preventing privilege escalation and unauthorised access at the most foundational level of the system. Without a functioning TCB, the security guarantees provided by higher-level software controls would have no reliable foundation to rest upon.

### Components of the TCB

The TCB typically consists of the trusted platform modules (TPM), the reference monitor, and elements of the operating system's kernel. The reference monitor is the part of the TCB that enforces the security rules; if it detects a violation, such as an attempt by one user mode program to access resources such as RAM or CPU registers allocated to another, it can and will shut down the system rather than allow a potential security violation to escalate. This willingness to shut down rather than permit a violation reflects the reference monitor's role as an uncompromising enforcer of security policy.

The operating system kernel contains the fundamental, core elements of the OS. These typically involve the functions that support creating and managing process IDs, managing main memory use by pocess, managing virtual memory and paging and managing the CPU and other essential hardaware subsystems. Together, the TPM, reference monior, and kernel elements form a layered defence at the lowest levels of the computing stack.

### Protecting the TCB Through Supply Chain and Configuration Management

Protecting the TCB requires a strong, secure IT and OT supply chain, which must then be brough and kept under configuration management. Updates to TCB elements should be taken extremely seriously and should never be allowed to happen without proper security, systems, and operational review and approval.

Even a seemingly straightforward change to a different make and mdoel of laptop or phablet computer for use across the organisation will bring a new TCB into the security baseline.

This means that hardware procurement decisions are not merely logistical or financial choices; they carry direct security implications because each new devices ontroduces a new TCB.

Configuration management processes must account for the TCB characteristics of every device in the organisations inventory. The supply chain itself must be trusted, because a compromised component introduced at any point in the supply chain could undermine the entire TCB.

### Key Takeaways

* the TCB is the lowest level enforcer of access control policies, preserving seperation of memory and CPU resources between process threads.
* The reference monitor will shut down the system rather than allow a potential security violation to escalate.
* The OS kernel manages process IDs, main memory, virtual memory and paging, and the CPU and other essential hardware subsystems.
* Even changing to a different make and model of laptop brings a new TCB intp the organisations security baseline.
