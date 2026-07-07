---
title: File Management
draft: false
tags:
  - os
  - computer-science
---
## Overview of the FS abstraction

| User's view                                                                           | Under the hood                                |
| ------------------------------------------------------------------------------------- | --------------------------------------------- |
| Uniform namespace                                                                     | Heterogeneous collection of storage devices   |
| Hierarchical structure                                                                | Flat address space (block numbers)            |
| Arbitrarily-sized files                                                               | Fixed-size blocks                             |
| Symbolic file names                                                                   | Numeric block addresses                       |
| File is one object                                                                    | File blocks may be "fragmented" across device |
| Access control                                                                        | Direct access to devices                      |
| Tools for:<br>- Formatting<br>- Defragmentation<br>- Backup<br>- Consistency checking |                                               |

## File Types

- Regular files
- Directories
- Device files
	- may be divided into
		- character devices - stream of bytes
		- block devices
- Streams/Pipes
- Some systems distinguish between regular file types
	- ASCII text files, binary files

## File Access Types (Patterns)

- Sequential access
	- read all bytes/records from the beginning
	- cannot jump around, could rewind or back up
	- convenient when medium was magnetic tape
- Random access
	- bytes/records read in any order
	- essential for data base systems
	- read can be ...
		- move file pointer (seek), then read or
			- lseek(location,...);read(...)
		- each read specifies the file pointer
			- read(location,...)

## Typical File Operations

- create
- delete
- open
- close
- read
- write
- append
- seek
- get attributes
- set attributes
- rename