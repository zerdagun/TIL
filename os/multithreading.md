# Multithreading

* Refers to the ability of an OS to support multiple concurrent paths of execution within a single process.

* All of the threads of a process share the state and resources of that process.

* The key states for a thread are Running, Ready and Blocked.

* The unit of dispatching is referred to as a **thread** or **lightweight process** and is interruptible.

* The unit of resource ownership is referred to as a **process** or **task**

* A single thread of execution per process is referred to as a **single threaded approach**.

* **Processes**: the unit or resource allocation and a unit of protection. A virtual address space that holds the process image.

* Each thread has: an execution stage, saved thread context when not running, en execution stack, spme per thread static storage for local variables, access to the memory and resources of its process.

## Benefits of Threads

* Takes less time to create a new thread than a process, less time to terminate a thread than a process, switching between two threads takes less time than switching between processes, threads enhance efficiency in communication between programs.

## Threads

* İşletim sistemlerinde CPU tarafından yürütülen en küçük işlem birimine **thread** denir.

* Suspending a process involves suspending all threads of the process.

* Termination of a process terminates all threads within the process.

* Thread operations associated with a change in thread state are: spawn, block, unblock, finish.

* All threads of a process share the same address space and other resources.

## Types of Threads

**User Level Thread (ULt)**

* All thread management is done by the application.
* The kernel is not aware of the existence of threads.

* Thread switching does not require kernel mode privileges, scheduling can be application specific, ULTs can run on any OS.

* when a ULT executes a system call, not only the thread is blocked but all of thread within the process are blocked.

* Jacketing: converts a blocking system call into a non blocking system call. Writing an application as multiple processes rather than multiple threads.

**Kernel Level Thread (KLT)**

* Thread management is done by the kernel. (Windows)

* The kernel can simultaneously schedule multiple threads from the same process on multiple processors. 

* If one thread in a process is blocked, the kernel can schedule another thread of the same process.

* The transfer of control from one thread to another within the same process requires a mode switch to the kernel.

**Combined Approaches**

* Thread creation is done in the user space.
* Bulk of scheduling and synchronization of thread is by the application.

**Relationship between threads and processes**

1:1 - Each thread of execution is a unique process with its own address space and resources. (Traditional UNIX implementations)

M:1 - A process defines an address space and dynamic resource ownership. Multiple threads may be created and executed within that process. (Linux)

1:M - Athread may migrate from one process environment to another. This allows a thread to be easily moved among distinct systems. (Clouds)

M:N - Combines attributes of M:1 and 1:M cases. (TRIX)

## Applications That Benefit

* Multithreaded native applications: characterized by having a small number of highly threaded processes.

* Multiprocess applications: characterized by the presence of many single threaded processes.

* Java applications

* Multiinstance applications: multiple instances of the application in parallel

## Windows 8 Processed and Thread Management

* Application: consists of one or more processes.
* Each process prodives the resources needed to execute a program.
* A thread is the entity within a process that can be scheduled for execution.
* A job  objects allows groups of processes to be managed as a unit.
* A thread pool is a collection of worker threads that efficiently execute asynchoronous callbacks on behalf of the application.

* A fiber is a unit of execution that must be manually scheduled by the application.

* User mode scheduling (UMS) is a lightweight mechanism that applications can use to schedule their own threads.

## Linux Threads

* does not recognize a distinction between threads and processes.

* the new process can be cloned so that it shares resources.

## Linux Namespaces

* a namespace enables a process to have a different view of the system than other processes that have other associated namespaces.

* six namespaces in linux: mnt, pid, net, ipc, uts, user.

## Processes and Threads

* processes are killed beginning with the lowest precedence first
* descending order of precedence are: foreground process, visible process, service process, background process, empty process

## Block
* A simple extension to a language, defines a self contained unit of work.
* enables the programmer to encapsulate complex functions
* scheduled and dispatched by queues
* dispatched ona first in first out basis
* can be associated with an event source, such as a timer, network socket, or file descriptor