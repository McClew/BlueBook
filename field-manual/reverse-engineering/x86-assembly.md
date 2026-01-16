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

# x86 Assembly

## Common Opcodes

The following table outlines the primary instructions used to manipulate data. Understanding these is the first step in tracing data flow through a programme.

<table><thead><tr><th width="108">Opcode</th><th width="147">Full Name</th><th>Description</th><th>Effect on Registers/Stack</th></tr></thead><tbody><tr><td>MOV</td><td>Move</td><td>Copies data from a source to a destination.</td><td>Updates the destination register; source remains unchanged.</td></tr><tr><td>LEA</td><td>Load Effective Address</td><td>Calculates an address (e.g., <code>[ebx+4]</code>) and stores it in a register.</td><td>Updates the destination register with an address, not the value at that address.</td></tr><tr><td>PUSH</td><td>Push onto Stack</td><td>Places a value onto the top of the stack.</td><td>Decrements the Stack Pointer (ESP) and writes the value to the new memory location.</td></tr><tr><td>POP</td><td>Pop from Stack</td><td>Removes the top value from the stack and stores it.</td><td>Increments the Stack Pointer (ESP) after moving the value to a register.</td></tr></tbody></table>

> Note: In x86 architecture, the stack "grows downwards" in memory. Therefore, a `PUSH` operation results in a lower memory address for the Stack Pointer.

***

## stdcall vs fastcall

Calling conventions define the "contract" between the function calling the code (the caller) and the function being executed (the callee). If you are following data in a debugger, knowing where to look for arguments is vital.

### stdcall (Standard Call)

Commonly used by the Windows API (Win32), this convention prioritises the stack for passing information.

* Argument Passing: All arguments are pushed onto the stack in right-to-left order.
* Stack Cleanup: The callee (the function itself) is responsible for cleaning up the stack before returning.
* Debugger Tip: Look for multiple `PUSH` instructions followed by a `CALL`. Inside the function, you will see a `RET X` (where X is the number of bytes to pop).

### fastcall

As the name suggests, this convention aims to increase performance by avoiding memory access (the stack) where possible.

* Argument Passing: The first few arguments (typically the first two) are passed directly into registers—usually ECX and EDX. Any remaining arguments are pushed onto the stack.
* Stack Cleanup: Like stdcall, the callee typically cleans the stack.
* Debugger Tip: If you see values being moved into `ECX` or `EDX` immediately before a `CALL`, you are likely looking at a fastcall convention.

### Comparison Summary

<table><thead><tr><th width="223">Feature</th><th width="181">stdcall</th><th>fastcall</th></tr></thead><tbody><tr><td>Primary Location</td><td>Stack</td><td>Registers (ECX, EDX) then Stack</td></tr><tr><td>Argument Order</td><td>Right-to-Left</td><td>Right-to-Left</td></tr><tr><td>Cleanup Responsibility</td><td>Callee</td><td>Callee</td></tr><tr><td>Typical Use Case</td><td>Windows API / DLLs</td><td>High-performance internal functions</td></tr></tbody></table>
