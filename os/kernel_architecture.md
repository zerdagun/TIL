# OS Architecture

## Microkernel VS Monolithic Kernel

kernel: core component of the operating system.

Monolithic Kernel: **all essential services** such as memory management, file systems, drivers run in **kernel space**.

Microkernel: **Only** the most essential services like IPC***1** and scheduling run in **kernel space** while everything else runs in **user space**.

**Monolithic Kernel**
examples: linux, unix, windows NT
* faster communication since evrything runs in the same space.
* mature,battle tested in production environments.
* risk of crashes. (a bug in one component can crash entire system.)
* difficult to debug or isolate faulty modules.

**MicroKernel**
examples: qnx, minix 3, seL4, fuchsia***2**
* better fault isolation and security
* easier module updates without rebooting
* slight performance overhead due to context switching and IPC
* less commonly used in general purpose OS but rising in embedded and secure systems

* ***1** IPC: Inter Process Communication. Mechanism that allows processes to communicate.
* ***2** Fuchsia: an open source operating system developed by Google.