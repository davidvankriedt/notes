---
title: Memory Management
draft: false
tags:
  - computer-science
  - os
---
Memory management within the OS keeps track of what memory is in use, and what memory is free. It also allocates free memory to processes when needed. It manages the transfer of memory content between RAM and disks.

Memory Hierarchy:
![[Screenshot 2026-07-28 at 15.54.07.png]]

There are 2 broad classes of OS memory management systems:
- OSs that transfer processes to and from external storage during execution (swapping or paging)
- OSs that don't - simple static OSs, like an embedded device, dumb phone, or smartcard.

# Virtual Memory

Developed to address the issues with memory management.

Like in an index-based file system, permit the process' actual memory contents to be scattered across real memory. It also creates bonus features:
- fine-grained swapping to disk.
- partial sharing of memory.

The process' view of memory is a virtual system.

Two classic variants:
- Paging
- Segmentation

Paging is now the dominant of the two. Some architectures support hybrids of the two schemes (e.g. Intel IA-32)

## Paging Overview

Divide physical memory into small chunks, called frames, which are evenly sized.

Divide each process' virtual address space, called pages, which are the same size as frames. Virtual memory addresses consist of a page number and offset within the page.

OS maintains a page table, which contains the frame location for each page. It is used by hardware to translate each virtual address to physical address. The mapping from virtual addresses and physical memory addresses is given by page table.

A process' physical memory does not have to be contiguous.

No external fragmentation. Small amounts of internal fragmentation - rounding up process memory region to a page.

Allows sharing by mapping several pages to the same frame.

Abstracts the physical organisation of memory - the programmer only deals with uniform virtual addresses.

## Memory Management Unit (MMU)

![[Screenshot 2026-07-29 at 11.29.26.png]]