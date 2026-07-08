---
title: File System Intervals
draft: false
tags:
  - computer-science
  - os
  - unix
---
## UNIX storage stack

![[Screenshot 2026-07-08 at 13.05.47.png]]


At the bottom of this stack lies the disk controller, which in the modern day tends to be a microcontroller on the drive that actually talks to the hardware. So the device driver doesn't directly speak with the hardware. The disk controller provides an interface for the hardware. It is the device driver's job to abstract multiple hardware interfaces that may require different protocols, and make them all uniform for the OS.

It's the file system's job to put a data structure on the storage medium and expose a friendly interface for the OS.

Buffer cache and Disk scheduler parts are optimisations. The buffer cache is to keep recently accessed disk blocks in memory. The disk scheduler, schedules disk accesses from multiple processes for performance and fairness.

The Virtual FS is there to abstract over different kinds of file system, providing a single interface to the OS.

The File descriptor and open file tables are there to keep track of files opened by user-level processes. It also matches syscall interface to VFS interface.

## Popular file systems
- FAT16
- FAT32
- NTFS
- Ext2
- Ext3
- Ext4

### Why are there so many?
- Different physical nature of storage devices
	- Ext3 is optimised for magnetic disks
	- JFFS2 is optimised for flash memory devices
	- ISO9660 is optimised for CDROM
- Different storage capacities
	- FAT16 does not support devices > 2GB
	- FAT32 becomes inefficient on drives > 32GB
	- ZFS, Btrfs is designed to scale to multi-TB disk arrays
- Different CPU and memory requirements
	- FAT16 is not suitable for modern PCs but is a good for for many embedded devices
- Proprietary standards
	- NTFS was a decent FS, but required a license

## Kinds of Storage Devices

- Flash memory
	- consists of a huge array of memory cells

Other devices use separate storage media:
- Tape spools
	- huge surface area, very slow access
- Spinning discs
	- compromise between size and access spend
- Magnetic media
- Optical media


## Devices and Locality

Many file systems are designed for spinning disks
- seek time
	- ~15ms worst case
- rotational delay
	- 8ms worst case for 7200rpm drive
- For comparison, disk-to-buffer transfer speed of a modern drive is ~10 microseconds per 4K block.
Conclusion: keep blocks that are likely to be accessed together close to each other - this is useful for other kinds of devices too.

## Implementing a file system

The FS must map symbolic file names into a collection of block addresses.

It must also keep track of:
- which blocks belong to which files.
- in what order the blocks form the file.
- which blocks are free for allocation.

Given a logical region of a file, the FS must track the corresponding block(s) on disk - stored in file system metadata.

## File Allocation Methods

A file is divided into "blocks", which is the unit of transfer to storage. Given the logical blocks of a file, there are methods for choosing where to put the blocks on disk.

#### Contiguous Allocation
- Easy bookkeeping (need to keep track of the starting block and length of the file)
- Increased performance for sequential operations
- Need the maximum size for the file at the time of creation
- As files are deleted, free space becomes divided into many small chunks (external fragmentation)
- Good for a read-only FS
- Example: ISO 9660 (CDROM FS)
![[Screenshot 2026-07-08 at 14.49.03.png]]

#### External and internal fragmentation

External fragmentation
- the space wasted external to the allocated memory regions
- memory space exists to satisfy a request but it is unusable as it is not contiguous

Internal fragmentation
- the space wasted internal to the allocated memory regions
- allocated memory may be slightly larger than requested memory; this size difference is wasted memory internal to a partition

#### Dynamic Allocation
- Disk space allocated in portions as needed
- Allocation occurs in fixed-size blocks
+ No external fragmentation
+ Does not require pre-allocating disk space
- File blocks are scattered across the disk
- Complex metadata management (maintain the collection of blocks for each file)
![[Screenshot 2026-07-08 at 14.49.59.png]]

##### Linked list allocation

Each block contains the block number of the next block in the chain. Free blocks are also linked in a chain.
- only single metadata entry per file
- best for sequentially accessed files
- poor for random access
- blocks end up scattered across the disk due to free list eventually being randomised
![[Screenshot 2026-07-08 at 14.58.02.png]]

##### File Allocation Table (FAT)
- Keep a map of the entire FS in a separate table
	- a table entry contains the number of the next block of the file
	- the last block in a file and empty blocks are marked using reserved values
- The table is stored on the disk and is replicated in memory
- Random access is faster (following the in-memory list)
- Requires a lot of memory for large disks
![[Screenshot 2026-07-08 at 15.06.30.png]]


##### Inode-based FS structure

Idea: separate table (index-node or i-node) for each file.
- only keep table for open files in memory
- fast random access

This is the __most popular__ FS structure today.
![[Screenshot 2026-07-08 at 15.13.49.png]]

###### Issues
- i-nodes occupy one or several disk areas
![[Screenshot 2026-07-08 at 15.16.53.png]]
- i-nodes are allocated dynamically, hence free-space management is required for i-nodes
	- use fixed-size i-nodes to simplify dynamic allocation

![[Screenshot 2026-07-08 at 15.36.29.png]]

Free-space management:
- Approach 1: linked list of free blocks in free blocks on disk
- Approach 2: keep bitmaps of free blocks and free i-nodes on disk 
![[Screenshot 2026-07-08 at 15.39.53.png]]

Free block list:
- list of all unallocated blocks
- background jobs can re-order list for better contiguity
- store in free blocks themselves
	- does not reduce disk capacity
- only one block of pointers need be kept in the main memory

Bit tables:
- individual bits in a bit vector flags used/free blocks
- 16GB disk with 512-byte blocks --> 4MB table
- May be too large to hold in main memory
- Expensive to search - optimisations possible, e.g. a two level table
- Concentrating (de)allocations in a portion of the bitmap has desirable effect of concentrating access
- Simple to find contiguous free space

## Implementing Directories

Directories are stored like normal files - directory entries are contained inside data blocks. The FS assigns special meaning to the content of these files:
- a directory file is a list of directory entries
- a directory entry contains file name, (optionally) attributes, and the file i-node number - maps human-oriented file name to a system-oriented name

### Fixed-size vs variable-size directory entries

Fixed-size directory entires:
- either too small, e.g. DOS 8+3 characters
- or waste too much space, e.g. 255 characters per file name

Variable-size directory entries:
- Freeing variable length entries can create external fragmentation in directory blocks - can compact when block is in RAM
- Must manage fragmentation problems inside directories

### Searching Directory Listings

Locating a file in a directory:
- Linear scan - implement a directory cache in software to speed-up search
- Hash lookup
- B-tree (100's of thousands entries)

## Storing file attributes

1. Disk addresses and attributes in directory entry - FAT
![[Screenshot 2026-07-08 at 15.54.49.png]]

2. Directory in which each entry just refers to an i-node - UNIX![[Screenshot 2026-07-08 at 15.55.35.png]]

## Trade-off in FS block size

File systems deal with 2 types of blocks:
- Disk blocks or sectors (usually 512 bytes)
- File system blocks 512 * 2^N bytes

Larger blocks require less FS metadata. Smaller blocks waste less disk space (less internal fragmentation).

Sequential Access - the larger the block size, the fewer I/O operations required

Random Access - The larger the block size, the more unrelated data loaded. Spatial locality of access improves the situation.

Choosing an appropriate block size is a compromise.