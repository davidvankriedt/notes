---
title: System Calls
draft: false
tags:
  - computer-science
  - os
---
System Calls are special function calls
- provides for a controlled entry into the kernel
- while in kernel, they perform a privileged operation
- returns to original caller with the result

The system call interface represents part of the abstract machine provided by the operating system.

## System Call Interface

- From the user's perspective
	- process management
	- file I/O
	- directories management
	- there are many more - `man syscalls`

![[Screenshot 2026-06-22 at 14.04.09.png]]![[Screenshot 2026-06-22 at 14.05.04.png]]

## Privileged-mode Operation

- to protect operating system execution, two or more CPU modes of operation exist
	- privileged mode (system-mode, kernel-mode)
		- all instructions and registers available
	- user mode
		- uses 'safe' subset of the instruction set
			- only affects the state of the application itself
			- they cannot be used to uncontrollably interfere with OS
		- only 'safe' registers are accessible
		- some memory regions may be unavailable

![[Screenshot 2026-06-22 at 14.13.21.png]]

in user mode, we can only see user-facing instructions, and such instructions can only affect the yellow registers, and the blue registers implicitly - the green registers are invisible. When we have privileged mode we can see additional instructions that have access to the additional state of the processor.

## Example Unsafe Instruction
- "cli" instruction on x86 architecture
	- disables interrupts
- example exploit
```
  cli /* disable interrupts */
  while (true)
	  /* loop forever */
```


There is only one register set - how is register use managed?

What does an application expect a system call to look like?

How is the transition to kernel mode triggered?

Where is the OS entry point (system call handler)?

How does the OS know what to do?


## System Call Mechanism Overview
- System call transitions triggered by special processor instructions
	- user to kernel
		- system call instruction
	- kernel to user
		- return from privileged mode instruction

why do we need system calls? why not simply jump into the kernel via a function call?
- function calls do not
	- change from user to kernel mode (and vice versa)
	- restrict possible entry points to secure locations
		- to prevent entering after any security checks

![[Screenshot 2026-06-22 at 14.32.36.png]]