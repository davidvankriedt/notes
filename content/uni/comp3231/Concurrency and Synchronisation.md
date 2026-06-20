---
title: Concurrency and Synchronisation
draft: false
tags:
  - computer-science
  - os
---
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
1. Mutual Exclusion
2. Progress (no process running outside its critical region may block another process)
3. Non-starvation
4. Generality

##### Solutions: 
- Disabling interrupts (disable interrupts before entering critical region, after leaving it enable interrupts) - it's simple, but only available in the kernel, delays everybody else, doesn't work on multi-core processor
### Test-and-set
Hardware support test-and-set (test memory cell X and set memory cell X, hardware guarantees instruction executes atomically, read-lock and set-lock happen in one instruction).

- we can use test-and-set to implement lock() and unlock() primitives
	- pros: simple, available at user-level - to any number of processors, to implement any number of lock variables
	- cons: busy waits (spin lock) - consumes CPU, starvation is possible when a process leaves its critical section and more than one process is waiting.

### Sleep/Wakeup:
-  if a user-level thread cannot take the lock, instead of spinning, it can make a "sleep" system call to wait without wasting CPU.
- when a thread releases the lock, it may need to call the "wakeup" system call to unblock other processes.
- accidentally calling "wakeup" when other threads are not sleeping has no effect.

#### The Producer-Consumer Problem
- also called the _bounded buffer_ problem
- a producer produces data items and stores the items in a buffer
- a consumer takes the items out of the buffer and consumes them.

	Issues: 
	- we must keep an accurate count of items in buffer
		- producer: should sleep when buffer is full, and wakeup when there is empty space in the buffer - consumer can call wakeup when it consumes the first entry of the full buffer.
		- consumer: should sleep when the buffer is empty, and wake up when there are items available - producer can call wakeup when it adds the first item to the buffer.


### Semaphores

Dijkstra (1965) introduced two primitives that are more powerful than simple sleep and wakeup alone.
- P(): _proberen_, from Dutch to test.
- V(): _verhogen_, from Dutch to increment.

##### How they work:
- if a resource is not available, the corresponding semaphore blocks any process waiting for the resource
- blocked processes are put into a process queue maintained by the semaphore (avoids busy waiting)
- when a process releases a resource, it signals this by means of the semaphore
- signalling resumes a blocked process if there is any, or stores the signal to be read by the next waiting task
- Wait (P) and signal (V) operations cannot be interrupted
- Complex coordination can be implemented by multiple semaphores.

##### Implementation
Define a semaphore as a record
```
	typedef struct {
		int count;
		struct process *L;
	} semaphore;
```
Assume two simple operations:
- __sleep__ suspends the process that invokes it.
- __wakeup__(P) resumes the execution of a blocked process __P__.

Semaphore operations now defined as

_wait_(S):
```
while (S.count <= 0) {
	add this process to S.L;
	sleep;
}
S.count--;
```

_signal_(S):
```
S.count++;

if (S.count <= 1) {
	remove a process P from S.L;
	wakeup(P);
}
```

Note each primitive is atomic, e.g. interrupts are disabled for each code fragment.

Summary:
- Semaphores can be used to solve a variety of concurrency problems
- however, programming with them can be error-prone
	- e.g. must signal for every wait for mutexes
		- too many, or too few signals or waits, or signals and waits in the wrong order, can have catastrophic results.


### Monitors
- to ease concurrent programming, Hoare (1974) proposed _monitors_.
	- a higher level synchronisation primitive
	- programming language construct
- __Idea__
	- a set of procedures, variables, data types are grouped in a special kind of module, a monitor.
		- variables and data types only accessed from within the monitor.
	- only one process/thread can be in the monitor at any one time
		- mutual exclusion is implemented by the compiler (which should be less error prone)

- when a thread calls a monitor procedure that has a thread already inside, it is queued and it sleeps until the current thread exits the monitor.![[Screenshot 2026-06-20 at 22.32.47.png]]

```
	monitor example:
		integer i;
		condition c;
		
		procedure producer ()
			...
			...
		end;
		
		procedure consumer ()
			...
			...
		end;
		
	end monitor;
```


simple example:
```
	monitor counter {
		int count;
		procedure inc() {
			count = count + 1;
		}
		procedure dec() {
			count = count - 1;
		}
	}
```

- compiler guarantees only one thread can be active in the monitor at any one time
- easy to see this provides mutual exclusion (no race condition on __count__).
- for instance, synchronised methods in Java.

### How do we block waiting for an event?
- we can use locks to block waiting for an object, held by another task.
- we can use semaphores to solve the producer/consumer problem directly.
- we would like a mechanism to block waiting for a kind of event (and also respect mutual exclusion)
	- e.g. in the producer-consumer problem
		- produce events
		- consume events
	- a blocked consumer is not waiting on just one producer
- _condition variables_

### Condition Variable
- to allow a process to wait within the monitor, a condition variable must be declared, as __condition x, y;__
- condition variable can only be used with the operations __wait__ and __signal__.
	- the operation
			__x.wait();__
		- means that the process invoking this operation is suspended until another invokes signal
		- another thread can enter the monitor while original is suspended
			__x.signal();__
		- the __x.signal__ operation resumes exactly one suspended process. If no process is suspended, then the signal operation has no effect.![[Screenshot 2026-06-20 at 22.42.52.png]]

### OS/161 Provided Synchronisation Primitives
- Locks
- Semaphores
- Condition Variables