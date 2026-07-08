---
title: The Virtual File System
draft: false
tags:
  - computer-science
  - os
  - unix
---
Older systems only had a single file system. They had file system specific calls - open, close, read, write. However, modern systems need to support many file system types - ISO9660 (CDROM), MSDOS (floppy), ext2fs, tmpfs.

## Supporting Multiple File Systems

Options:
- Change the file system code to understand different file system types - prone to code bloat, complex, non-solution
- Provide a framework that separates file system independent and file system dependent code - allows different file systems to be "plugged in".
![[Screenshot 2026-07-08 at 16.03.19.png]]


The Virtual File System (VFS)
- provides a single system call interface for many file systems - UFS, Ext2, XFS, DOS, ISO9660
- Transparent handling of network file systems - NFS, AFS, CODA
- File-based interface to arbitrary device drivers (/dev)
- File-based interface to kernel data structures (/proc)
- Provides an indirection layer for system calls
	- file operation table set up at file open time
	- points to actual handling code for particular type
	- further file operations redirected to those functions

The file system independent code deals with vfs and nodes![[Screenshot 2026-07-08 at 16.17.35.png]]

## VFS Interface

Linux and OS/161 differ slightly, but the principles are the same

Two major data types:
- VFS
	- represents all file system types
	- contains pointers to functions to manipulate each file system as a whole (e.g. mount, unmount) - form a standard interface to the file system
- Vnode
	- represents a file (inode) in the underlying filesystem
	- points to an in-memory copy of real inode
	- contains pointers to functions to manipulate files/inodes (e.g. open, close, read, write)

![[Screenshot 2026-07-08 at 16.20.03.png]]![[Screenshot 2026-07-08 at 16.20.23.png]]

## Roughly Object Oriented

The vfs/vnode types are like OO classes or interfaces. The particular file system implements sub-classes.

Each vfs/vnode object contains:
- generic data (superclass data)
- FS-specific data (subclass data)
- Function pointers to FS code (subclass methods)

This is a common pattern in OS implementations. Linux, OS/161 don't use C++ but "roll their own" - Apple has "Objective C".

![[Screenshot 2026-07-08 at 16.23.16.png]]![[Screenshot 2026-07-08 at 16.24.46.png]]![[Screenshot 2026-07-08 at 16.27.33.png]]