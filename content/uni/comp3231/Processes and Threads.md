---
title: Processed and Threads
draft: false
tags:
  - computer-science
  - os
---
### [[Processes]]
- Also called a task or job
- Memory image of an individual program
- "Owner" of resource allocated for program execution
- Encompasses one or more threads


### [[Threads]]
- Unit of execution
- Can be traced (list the sequence of instructions that execute)
- Belongs to a process (executes within it)

### Process and thread models of selected OSes
- Single process, single thread
	- MSDOS, simple embedded system
- Single process, multiple threads
	- OS/161 as distributed
- Multiple processes, single thread per processes
	- Traditional UNIX
- Multiple processes, multiple threads
	- Modern OSs (Linux, Solaris, Mac/Darwin, Windows)

#### Process Creation
###### Principal events that cause process creation:
1. System initialisation
	- Foreground processes (interactive programs)
	- Background processes (email server, web server, print server) - called a daemon (unix) or service (Windows)
2. Execution of a process creation system call by a running process
	- New login shell for an incoming ssh connection
3. User request to create a new process
4. Initiation of a batch job

#### Process Termination

###### Conditions which terminate processes
1. Normal exit (voluntary)
2. Error exit (voluntary)
3. Fatal error (involuntary)
4. Killed by another process (involuntary)

#### Implementation of Processes
 - A processes' information is stored in a _process control block_ (__PCB__)
 - The __PCPs__ form a process table - this might not actually be an array or table in memory.

#### Process/Thread States
- running
- blocked
- ready

![[Screenshot 2026-06-05 at 13.14.41 1.png]]
1. Process blocks for input
2. Scheduler picks another process
3. Scheduler picks this process
4. Input becomes available

#### Scheduler

Sometimes also called the dispatcher.
Has to choose a _Ready_ process to run, through a Ready Queue.


### Thread Usage

| Model                              | Characteristics                                                    |
| ---------------------------------- | ------------------------------------------------------------------ |
| Single-threaded server             | No parallelism, blocking system calls                              |
| Threaded server                    | Parallelism, blocking system calls                                 |
| State machine (event based server) | Parallel tasks, nonblocking system calls, interrupts/notifications |

### Thread Model
- Local variables are per thread
	- allocated on the stack
- Global variables are shared between all threads
	- allocated in data section
	- concurrency control is an issue
- dynamically allocated memory (malloc) can be global or local
	- program defined (the pointer can be global or local)

### Why threads?
- simpler to program than a state machine
- less resources are associated with them than multiple complete processes
	- cheaper to create and destroy
	- shares resources (especially memory) between them
	- simpler to co-ordinate (shared memory)
- Performance: Threads waiting for I/O can be overlapped with computing threads
	- Note if all threads are _compute bound_, then there is no performance improvement (on a uniprocessor)
- Threads can take advantage of the parallelism available on machines with more than one CPU (multiprocessor)

### Processes and threads summary
- OS provides process and thread mechanisms.
- The CPU is shared between processes and threads by repeated rapid thread-switching.
- Multiple tasks allow the CPU to stay busy when some tasks are waiting for an external event.
- Multi-threaded servers can manage multiple tasks within the one problem
	- an event-based server design can also manage multiple tasks on the one thread.