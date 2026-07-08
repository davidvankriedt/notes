---
title: Buffer Cache
draft: false
tags:
  - computer-science
  - os
  - unix
---
A __buffer__ is a temporary storage used when transferring data between two entities. Especially when the entities work at different rates, or when the unit of transfer is incompatible. For example, between application program and disk.![[Screenshot 2026-07-08 at 16.46.14.png]]

Note that here writes can return immediately after copying to kernel buffer, avoiding wait time. One can also implement read-ahead by pre-loading next block on disk to kernel buffer, which avoids having to wait until next read is issued.

## Cache

A cache is a fast storage used to temporarily hold data to speed up repeated access to the data. For example, main memory can cache disk blocks.![[Screenshot 2026-07-08 at 16.50.11.png]]

## Buffering and caching are related

Data is read into buffer; and extra independent cache copy would be wasteful. After use, block should be cached. Future access may hit cached copy. Cache utilises unused kernel memory space - may have to shrink, depending on memory demand.

## Unix Buffer Cache

On read
- hash the device#, block#
- check if match in buffer cache
- if yes, simply use in-memory copy
- if not, follow the collision chain
- if not found, we load block from disk into buffer cache![[Screenshot 2026-07-08 at 16.54.36.png]]

## Replacement

What happens when the buffer cache is full and we need to read another block into memory? We must choose an existing entry to replace. We need a policy to choose a victim:

- We can use First-in First-out
- Least Recently used, or others - timestamps required for LRU implementation

## File System Consistency

What if a file is read and written very frequently? This file is always "recently used". File data is expected to survive - this file needs to be written to disk eventually.

Generally, cached disk blocks are prioritised in terms of how critical they are to file system consistency. Directory blocks, inode blocks that are lost or invalid can corrupt the entire filesystem.
- Imagine corruption of the root directory or a home directory. These blocks are usually written to disk immediately.

Data blocks that are lost or invalid corrupt only the file that they are associated with. These blocks are written back to disk periodically.

Alternatively, we can use a write-through cache. All modified blocks are written immediately to disk. But this generates much more disk traffic - temporary files are written back, and multiple updates are not combined. This is used by DOS. It gave okay consistency when floppies were removed from drives, and when users where constantly resetting (or crashing) their machines. It's still used, for example in USB storage devices.