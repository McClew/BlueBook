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

# Windows Internals

## Windows Architecture <a href="#windows-architecture-at-a-high-level" id="windows-architecture-at-a-high-level"></a>

The below image showcases a simplified version of Windows' architecture.

<figure><img src="../../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

The simplified Windows architecture comprises both user-mode and kernel-mode components, each with distinct responsibilities in the system's functioning.

### User-mode Components <a href="#user-mode-components" id="user-mode-components"></a>

`User-mode components` are the parts operating system that don't have direct access to hardware or kernel data structures. They interact with system resources through APIs and system calls.

* `System Support Processes`: These are essential components that provide crucial functionalities and services such as logon processes (`winlogon.exe`), Session Manager (`smss.exe`), and Service Control Manager (`services.exe`). These aren't Windows services but they are necessary for the proper functioning of the system.
* `Service Processes`: These processes host Windows services like the `Windows Update Service`, `Task Scheduler`, and `Print Spooler` services. They usually run in the background, executing tasks according to their configuration and parameters.
* `User Applications`: These are the processes created by user programs, including both 32-bit and 64-bit applications. They interact with the operating system through [APIs](https://en.wikipedia.org/wiki/Windows_API) provided by Windows. These API calls get redirected to [NTDLL.DLL](https://en.wikipedia.org/wiki/Microsoft_Windows_library_files#NTDLL.DLL), triggering a transition from user mode to kernel mode, where the system call gets executed. The result is then returned to the user-mode application, and a transition back to user mode occurs.
* `Environment Subsystems`: These components are responsible for providing execution environments for specific types of applications or processes. They include the [Win32 Subsystem](https://en.wikipedia.org/wiki/Architecture_of_Windows_NT#Win32_environment_subsystem), [POSIX](https://en.wikipedia.org/wiki/Microsoft_POSIX_subsystem), and [OS/2](https://en.wikipedia.org/wiki/OS/2).
* `Subsystem DLLs`: These dynamic-link libraries translate documented functions into appropriate internal native system calls, primarily implemented in `NTDLL.DLL`. Examples include `kernelbase.dll`, `user32.dll`, `wininet.dll`, and `advapi32.dll`.

### Kernel-mode Components <a href="#kernel-mode-components" id="kernel-mode-components"></a>

`Kernel-mode components` are those parts of the operating system that have direct access to hardware and kernel data structures. These include:

* `Executive`: This upper layer in kernel mode gets accessed through functions from `NTDLL.DLL`. It consists of components like the `I/O Manager`, `Object Manager`, `Security Reference Monitor`, `Process Manager`, and others, managing the core aspects of the operating system such as I/O operations, object management, security, and processes. It runs some checks first, and then passes the call to kernel, or calls the appropriate device driver to perform the requested operation.
* `Kernel`: This component manages system resources, providing low-level services like `thread scheduling`, `interrupt and exception dispatching`, and `multiprocessor synchronization`.
* `Device Drivers`: These software components enable the OS to interact with hardware devices. They serve as intermediaries, allowing the system to manage and control hardware and software resources.
* `Hardware Abstraction Layer (HAL)`: This component provides an abstraction layer between the hardware devices and the OS. It allows software developers to interact with hardware in a consistent and platform-independent manner.
* `Windowing and Graphics System (Win32k.sys)`: This subsystem is responsible for managing the graphical user interface (GUI) and rendering visual elements on the screen.

***

## Windows API Call Flow <a href="#windows-api-call-flow" id="windows-api-call-flow"></a>

Malware often utilise Windows API calls to interact with the system and carry out malicious operations. By understanding the internal details of API functions, their parameters, and expected behavior, analysts can identify suspicious or unauthorized API usage.

Let's consider an example of a Windows API call flow, where a user-mode application tries to access privileged operations and system resources using the [ReadProcessMemory function](https://learn.microsoft.com/en-us/windows/win32/api/memoryapi/nf-memoryapi-readprocessmemory). This function allows a process to read the memory of a different process.

<figure><img src="../../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

When this function is called, some required parameters are also passed to it, such as the handle to the target process, the source address to read from, a buffer in its own memory space to store the read data, and the number of bytes to read. Below is the syntax of `ReadProcessMemory` WINAPI function as per Microsoft documentation.

{% code overflow="wrap" %}
```cpp
BOOL ReadProcessMemory(
  [in]  HANDLE  hProcess,
  [in]  LPCVOID lpBaseAddress,
  [out] LPVOID  lpBuffer,
  [in]  SIZE_T  nSize,
  [out] SIZE_T  *lpNumberOfBytesRead
);
```
{% endcode %}

`ReadProcessMemory` is a Windows API function that belongs to the `kernel32.dll` library. So, this call is invoked via the `kernel32.dll` module which serves as the user mode interface to the Windows API.

Internally, the `kernel32.dll` module interacts with the `NTDLL.DLL` module, which provides a lower-level interface to the Windows kernel. Then, this function request is translated to the corresponding Native API call, which is `NtReadVirtualMemory`. The below screenshot from `x64dbg` demonstrates how this looks like in a debugger.

<figure><img src="../../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

The `NTDLL.DLL` module utilises system calls (syscalls).

<figure><img src="../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

The `syscall` instruction triggers the system call using the parameters set in the previous instructions. It transfers control from user mode to kernel mode, where the kernel performs the requested operation after validating the parameters and checking the access rights of the calling process.

If the request is authorised, the thread is transitioned from user mode into the kernel mode. The kernel maintains a table known as the `System Service Descriptor Table (SSDT)` or the `syscall table (System Call Table)`, which is a data structure that contains pointers to the various system service routines.

These routines are responsible for handling system calls made by user-mode applications. Each entry in the syscall table corresponds to a specific system call number, and the associated pointer points to the corresponding kernel function that implements the requested operation.

The syscall responsible for `ReadProcessMemory` is executed in the kernel, where the Windows memory management and process isolation mechanisms are leveraged. The kernel performs necessary validations, access checks, and memory operations to read the memory from the target process. The kernel retrieves the physical memory pages corresponding to the requested virtual addresses and copies the data into the provided buffer.

Once the kernel has finished reading the memory, it transitions the thread back to user mode and control is handed back to the original user mode application. The application can then access the data that was read from the target process's memory and continue its execution.
