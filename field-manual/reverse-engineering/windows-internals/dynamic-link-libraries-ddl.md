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

# Dynamic-Link Libraries (DDL)

A Dynamic-link library (DLL) are a type of PE which expose an array of functions which can be exploited by malware.

## Import Functions <a href="#import-functions" id="import-functions"></a>

Import functions are functionalities that a binary dynamically links to from external libraries or modules during runtime. These functions enable the binary to leverage the functionalities offered by these libraries.

During malware analysis, examining import functions may shed light on the external libraries or modules that the malware is dependent on. This information aids in identifying the APIs that the malware might interact with, and also the resources such as the file system, processes, registry etc.

By identifying specific functions imported, it becomes possible to ascertain the actions the malware can perform, such as file operations, network communication, registry manipulation, and more.

Import function names or hashes can serve as IOCs (Indicators of Compromise) that assist in identifying malware variants or related samples.

Below is an example of identifying process injection using DLL imports and function names:

![](https://cdn.services-k8s.prod.aws.htb.systems/content/modules/227/process_injection_fn.png)

In this diagram, the malware process (`shell.exe`) performs process injection to inject code into a target process (`notepad.exe`) using the following functions imported from the DLL `kernel32.exe`:

* `OpenProcess`: Opens a handle to the target process (notepad.exe), providing the necessary access rights to manipulate its memory.
* `VirtualAllocEx`: Allocates a block of memory within the address space of the target process to store the injected code.
* `WriteProcessMemory`: Writes the desired code into the allocated memory block of the target process.
* `CreateRemoteThread`: Creates a new thread within the target process, specifying the entry point of the injected code as the starting point.

As a result, the injected code is executed within the context of the target process by the newly created remote thread. This technique allows the malware to run arbitrary code within the target process.

The functions above are WINAPI (Windows API) functions. Don't worry about WINAPI functions as of now. We'll discuss these in detail later.

We can examine the DLL imports of `shell.exe` (residing in the `C:\Samples\MalwareAnalysis` directory) using `CFF Explorer` (available at `C:\Tools\Explorer Suite`) as follows.

![](https://cdn.services-k8s.prod.aws.htb.systems/content/modules/227/imports_.png)

## Export Functions <a href="#export-functions" id="export-functions"></a>

* Export functions are the functions that a binary exposes for use by other modules or applications.
* These functions provide an interface for other software to interact with the binary.
