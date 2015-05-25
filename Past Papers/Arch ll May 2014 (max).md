1a - Memory protection is needed to stop one program from reading or writing to the data needed by another program or the monitor/OS. It must also allow the OS to read and write to any part of memory.

1b - The memory management unit (MMU) is a special piece of hardware which contains a table of flags for the currently running (user mode) process, which say whether or not the current process can read or write to given areas of memory. Memory is split into blocks called pages (normally 4096 bytes), which is marked readable/writable as a whole. Setting the flags in the MMU is a privileged operation, so only privileged programs can change them. Every time an unprivileged process tries to perform a memory access, the MMU checks the flags to see if it is allowed to do so.

1c - When an unprivileged process tries to perform a memory access, the MMU checks it's flags to see if it is allowed to do so. If not, it raises an interrupt, passing control back to the OS which can then decide what to do with the process.

1d - Page tables contain mappings between a process's virtual addresses and the actual physical addresses. Each page in a proccess's virtual address space corresponds to a page in the physical memory. They are stored in memory as part of the process control block.

1e - The translation lookaside buffer (TLB) is a piece of hardware and part of the MMU. It keeps a copy of a small subset of the mappings from the page table of the currently running process and can translate them very quickly. This means there doesn't have to be another read to memory to find the mapping every time an instruction or data read/write is executed.

1d - Because it has to be very fast, and is therefore very expensive.
