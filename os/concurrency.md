# Concurrency

**Arises in three different contexts:**
* multiple applications: invented to allow processing time to be shared among active applications
* structured applications: extension of modular design and structured programming
* operating system structure: os themselves implemented as a set of processes or threads

**some key terms**
* atomic operation: atomicity guarentees isolation from concurrent processes. a function or action implemented as a sequence of one or more instructions that appears to be indivisible; that is, no other process can see an intermediate state or interrupt the operation. bölünemez, kesilemez, araya girilemez işlemler.
* critical section: a section of a code within a process that requires access to shared resources and that must not be executed while another process is in a corresponding section of code
* deadlock: a situation in which two or more processers are unable to proceed because each is waiting for one of the others to do something
* livelock: a situation in which two or more processes continuouslt change their states in response to changes in the other processes without doing any useful work
* mutual exclusion: the requirement that when one process is in a critical section that accesses shared resources, no other process may be in a critical section that accesses any of those shared resources
* race condition: a situtation in which multiple threads or processes read and write a shared data item and the final result depends on the relative timing of their execution.
* starvation: a situation in which a runnable process is overlooked indefinitely by the scheduler; although it is able to proceed, it is never chosen.

* concurrent processes come into conflict when they are competing for use of the same resource. in the case of competing processes three control problems must be faced: the need for mutual exclusion, deadlock, starvation


**Requirements for Mutual Exclusion**
* must be enforced
* a process that halts must do so without interfering with other processes
* no deadlock or starvation
* a process must not be denied access to a critical section when there is no other process using it
* a process remains inside its critical section for a finite time only

**Mutual Exclusion: Hardware Support**
* compare and swap instruction: also called as compare and exchange isntruction, a compare is made between a memory value and a test value, if the values are the same a swap occurs, carried out atomically
* special machine instruction: advantages: applicable to any number of processes on either a single processor or multiple processors sharing main memory, simple and easy to verify, it can be used to support multiple critical sections; each critical section can be defined by its own variable.
* special machine instruction: disadvantages: busy waiting is employed, thus while a process is waiting for access to a critical section it continues to consume processor time
* starvation is possible when a process leaves a critical section and more than one process is waiting
* deadlock is possible

**Semaphore**
* birden fazal threadin aynı kaynağa saldırmasını engellemek için kullanılan yöntem
* a variable that has an integer value upon which only three operations are defined.
1- may be initialized to a nonnegative integer value
2- the semWait operaiton decrements the value
3- the semSignal operation increments the value
* strong semaphores: the process that has been blocked the longest is released from the queue first (FIFO)
* weak semaphore: order of the queue is not specified

**Monitors**
* içine aynı anda sadece tek bir threadin girebildiği nesne.
* easier to control than semaphores
* process enters monitor by invoking one of its procedures
* only one process may be executing in the monitor one at a time
* synchronization: achieved by the use of condition variables that are contained within the monitor and accessible only within the monitor
* condition variables are operated on by two functions: cWait(c): suspend execution of the calling procrss on condition c. csignal(c): resume execution of some process blocked after a cwait on the same condition

**Message Passing**
* when processes interact with one another two fundamental requirements must be satisfied: synchronization and communication.
* synchronization for enforce mutual exclusion.
* communication for exchange information
* an approach to providing both of these functions
* a process sends information in the form of a message to another process designated by a destination
* a process receives info by executing the receive primite, indicating the source and the message

**Synchronization**
* communication of a message between two processes
* the receiver cannot receive a message until it has been sent by another process
* when a receive primite is executed in a process there are two possibilites:
1 - if there is no waiting message, the process is blocked until a message arrives or the process continues to execute, abandoning the attempt to receive
2 - if a message has previously been sent, the message is received and execution continues

**Blocking Send, Blocking Receive**
* both sender and receiver are blocked until the message is delivered
* called rendezvous
* allows for tight synchronization between processes

**Nonblocking Send**
* Nonblocking send, blocking receive
- sender continues on but receiver is blocked until the requested message arrives
- most useful combination
- sends one or more messages to a variety of destinations as quickly as possible
* Nonblocking send, nonblocking receive
- neither party is required to wait

**Addressing**
* schemes for specifying processes in send and receive primitives fall into categories: direct adressing, indirect addressing
**Direct Addressing**
* send primitive includes a specific identifier of the destination process
* receive primitive can be handled by in one of two ways: require that the process explicitly designate a sending process, implicit addressing
**Indirect Addressing**
* messages are sent to a shared data structure consisting of queues that can temporarily  hold messages
* queues are referred to as maiboxes
* one process sends a message to the mailbox and the other process picks up the message from the mailbox
* allows greater flexibility in the use of messages

## Readers/Writers Problem
* a data is shared among many processes
* some processes only read the data (readers)
* some only write to the data area (writers)

**Conditions that must be satisfies:**
* any number of readers may simultaneously read the file
* only one writer at a time may write to the file
* if a writer is writing to the file, no reader may read it
