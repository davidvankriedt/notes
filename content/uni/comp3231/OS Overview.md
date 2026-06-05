---
title: OS Overview
draft: false
tags:
  - computer-science
  - os
---

## What is an [[Operating System]]?
1. __Abstraction__: It is an abstract machine that extends basic hardware with added functionality, providing high-level abstractions - hiding details of hardware, making application code portable.

2. __Resource manager__: It is also a resource manager, allocating resources to users and processes.

The [[Operating System]] is the software in [[privileged mode]].

#### Kernel
The [[kernel]] is the portion of the operating system that is running in privileged mode. 
- It contains fundamental functionality (what's required to implement other services and provide security).
- It contains most frequently used functions
- Also called the nucleus or supervisor

#### Privilege
Applications should __not__ be able to interfere or bypass the operating system.
- OS can enforce the "extended machine"
- OS can enforce its resource allocation policies
- Prevent applications from interfering with each other

#### System Libraries
They are simply that, libraries of support functions (you can write them yourself in C, etc) - e.g. `strcmp(), memcpy()`.

Only a subset of library functions are actually system calls:
- system calls: `open(), close(), read(), write()`.
- hybrids: `fprintf(), readline(), malloc()` (only perform a system call if necessary)

System calls are in the library for convenience.

OS functions the same way as ordinary software, but it has more privileges.

OS relinquishes control of the processor to execute other programs. Reestablishes control after: system calls, interrupts (especially timer interrupts)