---
title: File Management
draft: false
tags:
  - os
  - computer-science
  - unix
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

## File Organisation and Access

Given an operating system that supports unstructured files that are a stream-of-bytes, programmers can organise the contents of a programs files. e.g. Executable Linkable Format (ELF)
![[Screenshot 2026-07-08 at 10.16.26.png]]

Some possible access patterns:
- Read the whole file
- Read individual records from a file (sequence of bytes containing the record)
- Read records preceding or following the current one
- Retrieve a set of records
- Write a whole file sequentially
- Insert/delete/update records in a file

Programmers are free to structure the file to suit the application.


## Criteria for File Organisation

Things to consider when designing file layout:
- rapid access
	- needed when accessing a single record
	- not needed for batch mode
		- read from start to finish
- ease of update
	- file on CD-ROM will not be updated, so this is not a concern
- economy of storage
	- should be minimum redundancy in the data
	- redundancy can be used to speed access such as an index

## File Directories

File Directories provide mapping between file name and the files themselves. They contain information about files - attributes, location, ownership. The directory itself is a file owned by the operating system.

## Typical Directory Operations

- create
- delete
- opendir
- closedir
- readdir
- rename
- link
- unlink

## Nice properties of UNIX naming

- simple, regular format
	- names referring to different servers, objects, etc, have the same syntax.
		- regular tools can be used where specialised tools would be otherwise needed.
- location independent
	- objects can be distributed or migrated, and continue with the same names.

## File Sharing

In a multiuser system, files are allowed to be shared among users. This arises two issues: access rights, and the management of simultaneous access.

#### Access Rights

None:
- users may not know of the existence of the file
- user is not allowed to read the directory that includes the file

Knowledge:
- user can only determine that the file exists and who its owner is

Updating:
- the user can modify, delete, and add to the file's data. This includes creating the file, rewriting it, and removing all or part of the data

Changing protection:
- the user can change the access rights granted to other users

Deletion:
- the user can delete the file

Owners:
- the owner user has all rights previously listed
- they may grant rights to others using the following classes of users:
	- specific users
	- user groups
	- all users - for public files

#### Simultaneous Access

Most OSes provide mechanisms for users to manage concurrent access to files - e.g.  `flock()`, `lockf()`, system calls.

Typically:
- a user may lock entire file when it is to be updated.
- user may lock individual records during an update.

Mutual exclusion and deadlock are issues for shared access.