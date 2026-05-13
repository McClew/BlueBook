# x86 Assembly

## Common Opcodes

The following table outlines the primary instructions used to manipulate data. Understanding these is the first step in tracing data flow through a programme.

<table><thead><tr><th width="108">Opcode</th><th width="147">Full Name</th><th>Description</th><th>Effect on Registers/Stack</th></tr></thead><tbody><tr><td>MOV</td><td>Move</td><td>Copies data from a source to a destination.</td><td>Updates the destination register; source remains unchanged.</td></tr><tr><td>LEA</td><td>Load Effective Address</td><td>Calculates an address (e.g., <code>[ebx+4]</code>) and stores it in a register.</td><td>Updates the destination register with an address, not the value at that address.</td></tr><tr><td>PUSH</td><td>Push onto Stack</td><td>Places a value onto the top of the stack.</td><td>Decrements the Stack Pointer (ESP) and writes the value to the new memory location.</td></tr><tr><td>POP</td><td>Pop from Stack</td><td>Removes the top value from the stack and stores it.</td><td>Increments the Stack Pointer (ESP) after moving the value to a register.</td></tr></tbody></table>

> Note: In x86 architecture, the stack "grows downwards" in memory. Therefore, a `PUSH` operation results in a lower memory address for the Stack Pointer.

***

## Registers

Registers are the variables in the assembly language. The size of each register in x86 architecture is 32 bits. Registers are located in the processor and each processor can have its own proprietary registers.

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

### Data Registers

Data registers are the ones that contain data.

<table><thead><tr><th width="254.00006103515625">Register</th><th>Description</th></tr></thead><tbody><tr><td><strong>EAX (Accumulator Register)</strong></td><td>The most basic register used in arithmetic operations is the "EAX" register. It stores the results of arithmetic operations and the return values of functions. For example, it is used for operations such as addition and multiplication.</td></tr><tr><td><strong>EBX (Base Register)</strong></td><td>It is the register that holds the base address of the program.</td></tr><tr><td><strong>ECX (Counter Register)</strong></td><td>The “<strong>ECX</strong>” is the register that is used as counter. It is used in loop and string operations.</td></tr><tr><td><strong>EDX (Data Register)</strong></td><td>It is a register that is generally used for holding data. It is also used in I/O (Input/Output) operations.</td></tr></tbody></table>

### Pointer Registers

Pointer registers are the ones that hold memory addresses.

<table><thead><tr><th width="227.5999755859375">Register</th><th>Description</th></tr></thead><tbody><tr><td><strong>EBP (Base Pointer)</strong></td><td>EBP is the one that holds the lowest address of the Stack and is used for local variables.</td></tr><tr><td><strong>ESP (Stack Pointer)</strong></td><td>It is the register that holds the top address of the stack. Displays the last element that entered the Stack.</td></tr><tr><td><strong>EIP (Instruction Pointer)</strong></td><td>The EIP register may be the most important register as it holds the address of the next instruction to be executed in the program flow. In other words, if the value of this register is changed, the flow of the program can be interfered with.</td></tr><tr><td><strong>2.1.9. Index Registers</strong></td><td>Index registers are used for index information storage.</td></tr><tr><td><strong>ESI (Source Index)</strong></td><td>It is the register that holds the source index information for string operations. It holds the address of where the data will be read.</td></tr><tr><td><strong>EDI (Destination Index)</strong></td><td>It is the register that holds the destination index information for string operations. It holds the address of where the data will be written.</td></tr></tbody></table>

### Segment Registers

Segment registers are the registers used to hold addresses of specific segments in memory.

<table><thead><tr><th width="207.5999755859375">Register</th><th>Description</th></tr></thead><tbody><tr><td><strong>Stack Segment (SS)</strong></td><td>It is the segment register that holds the base location address of the stack.</td></tr><tr><td><strong>Code Segment (CS)</strong></td><td>It is the register which is known as “<strong>.text</strong>” and it holds the address of the code segment used for data access.</td></tr><tr><td><strong>Data Segment (DS)</strong></td><td>It is the register which is also known as “<strong>.data</strong>” and it holds the address of the data segment which is the default variable location for data access.</td></tr><tr><td><strong>Extra Segment (ES)</strong></td><td>It is the register that holds the address of the extra segment used during string operations.</td></tr></tbody></table>

### EFLAGS Register - Status Flags

The EFLAGS register, unlike other registers, is a special register where each bit has a different meaning. The values of the bits of this register allow the CPU operations to be controlled and monitored.

<table><thead><tr><th width="183.60003662109375">Flag</th><th>Description</th></tr></thead><tbody><tr><td><strong>Adjust Flag (AF)</strong></td><td>It is the flag that is set when there is a transfer from the 3rd bit to the 4th bit in arithmetic operations.</td></tr><tr><td><strong>Carry Flag (CF)</strong></td><td><p>It is the flag that is set in arithmetic operations when the value of the register is more than the maximum value or if the value is less than the minimum value of the register. For example, the description over 4 bits is as follows:<br><br><strong>Example 1</strong>: </p><p>Initially: “<strong>CF = 0</strong>”</p><p>1111 + 0001 = 0000 (CF = 1)</p><p>0000 - 0001 = 1111 (CF = 0)<br><br><strong>Example 2</strong>: </p><p>Initially: “<strong>CF = 0</strong>”</p><p>0000 - 0001 = 1111 (CF = 1)<br><br><strong>Example 3</strong>: </p><p>Initially: “<strong>CF = 0</strong>”</p><p>0111 + 0001 = 1000 (CF = 0)</p><p>1000 - 0001 = 0111 (CF = 0)</p></td></tr><tr><td><strong>Direction Flag (DF)</strong></td><td>It is the flag that determines the direction in the transport and comparison of string data. The string operation is performed from left to right in case of “<strong>DF = 0</strong>”, and from right to left in case of “<strong>DF = 1</strong>”.</td></tr><tr><td><strong>Interrupt Flag (IF)</strong></td><td>It is the flag that determines whether external interruptions are taken into consideration and therefore it is the flag that determines whether the necessary operation is implemented. Keyboard entry would be a good example to the external interruption. Interruptions are ignored in case of "<strong>IF = 0</strong>" and considered disabled, and are applied to the process in case the "<strong>IF = 1</strong>" state.</td></tr><tr><td><strong>Overflow Flag (OF)</strong></td><td>The overflow flag is set when a positive value for the signed integer is too large to be represented in the register, or when a negative value is too small.</td></tr><tr><td><strong>Parity Flag (PF)</strong></td><td><p>It is the flag that shows the total number of "<strong>1</strong>" bits in the results of arithmetic operations. If the total number of “1” bits is even, it becomes “PF = 1”. If the total number of “<strong>1</strong>” bits is odd, it becomes “<strong>PF = 0</strong>”.<br><br><strong>Example 1</strong>: </p><p>10111100 + 00010001 = 11001101 (PF = 0)<br></p><p><strong>Example 2</strong>: </p><p>10111100 + 00010000 = 11001100 (PF = 1)</p></td></tr><tr><td><strong>Sign Flag (SF)</strong></td><td>It is the flag that indicates whether the result of an arithmetic operation is negative or positive. If the result of the arithmetic operation takes a negative value, the sign flag is set as “<strong>SF = 1</strong>”. In case of a positive result, the sign flag will be in the state of “<strong>SF = 0</strong>”.</td></tr><tr><td><strong>Trap Flag (TF)</strong></td><td>It is the flag that allows the processor to set the operating mode as single-step mode. The debugger program sets this flag to run each command one by one. In this way, each command executed by the processor at the assembly level can be executed step by step.</td></tr><tr><td><strong>Zero Flag (ZF)</strong></td><td>It is the flag set depending on whether the result of the arithmetic or the comparison operations is "<strong>0</strong>" (zero). If the result of the operation is “<strong>0</strong>”, then the  zero flag is set as “<strong>ZF = 1</strong>”. If the operation result is other than zero, then the zero flag is not set “<strong>ZF = 0</strong>”.<br><br>In this part of the training, we have covered the segment registers and status flags, which are the continuation of register. In the next part of the training, "<strong>X86 Assembly Language and CPU Instructions</strong>" will be covered.</td></tr></tbody></table>

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
