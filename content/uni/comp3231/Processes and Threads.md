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

### Concurrency issues
Since threads share global variables, 2 threads accessing the same global variables at the same time will result in a race condition. This can still happen in different processes, because even though processes don't share global variables, a process' stack is mirrored in the kernel, and so if 2 processes interact with the kernel and do the same thing, there is a race condition there as well.

### [[Critical Region]]
Critical regions are regions of code that:
1. Access a shared resource
2. Correctness relies on the shared resource not being concurrently modified by another thread/process/entity.

- We can control access to the shared resource by controlling access to the code that accesses the resource.
- Uncoordinated entry to the critical region results in a race condition ---> incorrect behaviour, deadlock, lost work, etc.

##### Critical Region Solutions
Conditions required of any solution to the critical region problem:
1. Mutual Exclustion
2. Progress (no process running outside its critical region may block another process)
3. Non-starvation
4. Generality

##### Solutions: 
- Disabling interrupts (disable interrupts before entering critical region, after leaving it enable interrupts) - it's simple, but only available in the kernel, delays everybody else, doesn't work on multi-core processor
- Hardware support (test memory cell X and set memory cell X, hardware guarantees instruction executes atomically, read-lock and set-lock happen in one instruction) - simples, available at user-level to any number of processors and to implement any number of lock variables, but busy waits (spin lock) which consumes CPU and starvation might be possible when a process leaves its critical section and more than one process is waiting.
- Sleep/Wakeup:
	- if a user-level thread cannot take the lock, instead of spinning, it can make a "sleep" system call to wait without wasting CPU.
	- when a thread releases the lock, it may need to call the "wakeup" system call to unblock other processes.
	- accidentally calling "wakeup" when other threads are not sleeping has no effect.