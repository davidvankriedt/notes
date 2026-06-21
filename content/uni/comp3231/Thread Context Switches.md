---
title: Thread Context Switches
draft: false
tags:
  - computer-science
  - os
---
A context switch can refer to
- a switch between threads
	- involving saving and restoring of state associated with a thread
- a switch between processes
	- involving the above, plus extra state associated with a process.
		- e.g. memory maps.

a switch between process/thread can happen any time execution enters the OS
- on a system call
	- mandatory if system call blocks or on exit();
- on an exception
	- mandatory if the process cannot continue
- on an interrupt
	- triggering a dispatch is the main purpose of the timer interrupt

a thread switch can happen between any two instructions of a user-level program
- note instructions do not equal program statements