1a. Memory protection is needed to stop one process from accidentally (or intentionally) overwriting the memory in use by another process. It is also needed to stop one process accessing potentially sensitive information being handled by another.

b. The MMU keeps a cached copy of a subset of the page tables. If a process requests a page, its entry in the page table will be read. If that process has the correct flag set for the operation it's trying to perform against the page it's trying to perform it on, the operation will be allowed. Otherwise, the operation is prohibited, protecting the memory.

c. If a user process tries to access prohibited memory (assuming virtualisation isn't being used), the MMU will raise a segmentation violation. The kernel will send this to the offending process and then decide whether to kill that process or ignore the violation. In either case, the process won't be allowed to access the prohibited memory location.

d. Page tables are stored in full in memory (and potentially on disk after swapping). There is also a cached copy of recently used page table entries stored in the TLB. The page tables record the physical page number, a list of processes allowed to access that page, the virtual page number they use to refer to it, and the permissions they have to read, write or execute data stored in it.

e. The TLB is a piece of specialised hardware in the MMU to enable memory virtualisation. It does this by keeping a cached copy of a subset of the page tables, and translating very quickly between virtual and physical addresses. When a process access to a location, the TLB translates the address it uses into the physical address of that memory using the value stored in page tables, potentially reading them from main memory or disk first.

f. The cache in a TLB is small because it will only be effective with very fast memory, and memory that fast is very expensive.

2a. CPU is not a limited resource in a large multiprocessor computer. It is unlikely for a program to bottleneck on the CPU in this kind of machine, because so much processing power is available.

CPU is not very limited in a normal desktop computer. The everyday tasks the computer performs will rarely be computationally expensive enough to use all the available CPU power.

CPU is fairly limited in a mobile phone. Because the CPU in phones is designed to be small, energy-efficient and cool without active cooling, many applications that would run on a desktop machine would be slowed down by the processor in a mobile phone.

b. Memory is limited in a large multiprocessor computer. While there may be enough of it, the task of communication between processors using the memory and caches can cause a bottleneck, especially if not done properly.

Memory is typically not a limited resource in a modern desktop PC. This is especially true thanks to swapping, which means that even if more memory is needed than available, the programs can still all run. However, typical computers don't run big enough programs to use all the available memory.

Memory is more limited in mobile phones, though less so as phones become more powerful. Although not as much memory is likely to be available than in a desktop, the applications that run on a phone are also likely to be smaller in memory than their desktop equivalents.

c. Energy is a fairly limiting factor in large multiprocessor computers, in the sense that a big enough computer consumes a lot of power and generates a lot of heat, so reducing these will save money. It is therefore limited in that its use is minimised as much as possible without affecting performance. However, it isn't limited in the sense that there is a limited amount of it available.

Energy is not a limiting factor in a normal desktop. The amount of energy they consume is limited only by the capacity of the PSU, since the amount of money this electricity costs is negligible.

Energy is a very limiting factor in a mobile phone. The only power available comes from the battery, so the OS must waste as little as possible to make the battery last longer.

d. This is desirable so that programs written for one piece of hardware will also work on another piece of hardware running the same operating system. If the programmer had to interface directly with the hardware, as was the case in early computers, the program would have to be rewritten completely to run on a different piece of hardware. If the program can interface with standard parts of the OS, then it will be able to run wherever that OS runs.

e. Another desirable property is

f. The OS and system libraries perform different tasks. The purpose of system libraries is to offer implementations of standard functions
