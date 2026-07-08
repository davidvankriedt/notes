---
title: File Descriptor & Open File Tables
draft: false
tags:
  - computer-science
  - os
  - unix
---
![[Screenshot 2026-07-08 at 16.29.35.png]]


## File Descriptors

In UNIX, each open file has a file descriptor. Read/Write/lseek/... use them to specify which file to operate on.

State associated with a file descriptor:
- File pointer (offset)
	- determines where in the file the next read or write is performed
- Mode
	- was the file opened read-only, etc...

#### Options for file descriptors

##### Using vnode numbers as fd

One option is to use vnode numbers as file descriptors and add a file pointer to the vnode. However, what happens when we concurrently open the same file twice? We should get two separate file descriptors and file pointers.

##### Single global open file array
Another options is single global open file array, where fd is an index into the array, and entries contain file pointer and pointer to a vnode![[Screenshot 2026-07-08 at 16.36.51.png]]

Problems with this are that file descriptor 1 is stdout. Stdout is a console for some processes, and a file for others. Therefore, entry 1 needs to be different per process.

##### Per-process file descriptor array

The third option is a per-process file descriptor array. Each process has its own open file array - contains fp, v-ptr. In this case Fd 1 can point to any vnode for each process (console, log file).

![[Screenshot 2026-07-08 at 16.41.08.png]]

The issue: Fork defines that the child shares the file pointer with the parent. Dup2 also defines the file descriptors share the file pointer. With per-process table, we can only have independent file pointers, even when accessing the same file.

##### Per-Process fd table with global open file table

The final option is using a per-process file descriptor array, which contains pointers to open file table entry. The open file table array contains entries with a fp and pointer to a vnode. It provides both shared file pointers and independent file pointers if required. 

Example: all three fds refer to the same file, two share a file pointer, one has an independent file pointer.![[Screenshot 2026-07-08 at 16.44.36.png]]