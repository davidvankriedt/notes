---
title: MIPS R3000
draft: false
tags:
  - computer-science
  - os
---
- sequel to the R2000
- Developed by MIPS Computer Systems, 1988
- widely used through the 90s
	- silicon graphics IRIS
	- DEC DECstation
	- Sony PlayStation

- Load/store architecture
	- no instructions that operate on memory except load and store
	- simple load/stores to/from memory from/to registers
	- delay of one instruction after load before data available in destination register
		- there must always be another instruction between a load from memory and the subsequent use of the register.

- all instructions are encoded in 32-bit

- branching and jumping have a branch delay slot

 
![[Screenshot 2026-06-21 at 18.01.39.png]]


Why the delay features?
- tension between software design agenda and silicon implementation characteristics:
	- language design is usually in-order.
	- silicon circuit can do *many* calculations at once, but cannot *communicate* those results at once.
- usual solution: CPU hides its out-of-order nature.
	- exceptions: MIPS delay slots, Itanium "bundles".
	- some issues sneak out, e.g. timing unpredictability.
		- arguably including Spectre + Meltdown.
	![[images.jpg|661]]

However, microprocessors/microcontrollers (low energy, affordable) execute instructions in order.


## Coprocessor 0
- the processor control registers are located in CP0
	- exception/interrupts management registers
	- translation management registers
- CP0 is manipulated using mtc0 (move to) and mfc0 (move from) instructions
	- mtc0/mfc0 are only accessible in kernel mode.
- exception management
	- c0_cause - cause of the recent exception
	- c0_status - current status of the CPU
	- c0_epc - address of the instruction that caused the exception
	- c0_badvaddr - address accessed that caused the exception
- Miscellaneous
	- co_prid - processor identifier
- memory management
	- c0_index
	- c0_random
	- c0_entryhi
	- c0_entrylo
	- c0_context

![[Screenshot 2026-06-22 at 14.43.43.png]]![[Screenshot 2026-06-22 at 14.44.00.png]]![[Screenshot 2026-06-22 at 14.45.37.png]]![[Screenshot 2026-06-22 at 14.46.34.png]]![[Screenshot 2026-06-22 at 14.47.29.png]]

In MIPS, the general exception memory address is 0x80000080