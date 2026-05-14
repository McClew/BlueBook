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
---

# Processes

In the simplest terms, a process is an instance of an executing program. It represents a slice of a program's execution in memory and consists of various resources, including memory, file handles, threads, and security contexts.

<figure><img src="../../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

Each process is characterized by:

* `A unique PID (Process Identifier)`: A unique Process Identifier (PID) is assigned to each process within the operating system. This numeric identifier facilitates the tracking and management of the process by the operating system.
* `Virtual Address Space (VAS)`: In the Windows OS, every process is allocated its own virtual address space, offering a virtualised view of the memory for the process. The VAS is sectioned into segments, including code, data, and stack segments, allowing the process isolated memory access.
* `Executable Code (Image File on Disk)`: The executable code, or the image file, signifies the binary executable file stored on the disk. It houses the instructions and resources necessary for the process to operate.
* `Table of Handles to System Objects`: Processes maintain a table of handles, a reference catalogue for various system objects. System objects can span files, devices, registry keys, synchronization objects, and other resources.
* `Security Context (Access Token)`: Each process has a security context associated with it, embodied by an `Access Token`. This `Access Token` encapsulates information about the process's security privileges, including the user account under which the process operates and the access rights granted to the process.
* `One or More Threads Running in its Context`: Processes consist of one or more threads, where a thread embodies a unit of execution within the process. Threads enable concurrent execution within the process and facilitate multitasking.
