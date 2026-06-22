---
title: Basic computer architecture
draft: false
tags:
  - computer-science
  - os
---
__CPU__ - low data storage, performs operations
__Hard drive__ - holds lots of storage, slow
__RAM__ - holds little storage, fast
__SSD__ - like a hard drive but faster and more durable
__Bus__ - What connects components together (parallel and serial)
__Registers__ - Memory slots that live within the CPU (fixed number), faster than RAM
__Machine Instructions__ - Low-level, binary commands executed directly by a computer's CPU.
__Interrupts/Exceptions__ - 


## A Simple Model of CPU Computation

- The fetch-execute cycle
	- load memory contents from address in program counter (PC)
		- the instruction
	- execute the instruction
	- increment PC
	- repeat
	
![[Screenshot 2026-06-22 at 14.09.56.png]]
- stack pointer (SP)
- status register
	- condition codes
		- positive result
		- zero result
		- negative result
- general purpose registers
	- holds operands of most instructions
	- enables programmers (compiler) to minimise memory references.

![[Screenshot 2026-06-22 at 14.13.21.png]]