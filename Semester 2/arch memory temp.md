####Memory

######Memory Allocation
When a process runs, it must be assigned, or *allocated*, memory. Memory assigned when the process is initialised is the *static allocation*. Memory assigned while the process is running is the *dynamic allocation*. This didn't exist in early computers; processes could only use the memory they said they would need when they were created. Memory can also be dynamically freed while the process is running, and all of its memory freed when it completes.

Because it is a process, the kernel also needs to be statically and dynamically assigned memory.

In early operating systems with no dynamic allocation, processes had to be a fixed size and a fixed number of them could run at a time. Early languages such as FORTAN reflect this in only allowing data types with statically declared size. Modern languages have dynamic allocation, implemented using *implicit memory management*, where the language controls how much memory each object has, or *explicit memory management*, where the programmer uses commands such as malloc to allocate memory.

Free memory above the kernel allows it to grow dynamically, and free memory within each process allows data and stack to grow. This is how memory would be layed out in an early dynamic system:
![](http://gyazo.com/5c806358d7e705881e52c8a41f890085.png)
Before dynamic allocation, languages could not have a stack. This is true of FORTRAN, which can't use recursion as a result.

The earliest and simplest static memory layout is called *partitioning*, where areas of memory of fixed size are created at boot time.
![](http://gyazo.com/2406bb1210b1cf76a33b6c81df35cdb7.png)
When a process is created and declares how much memory it will need, it is loaded into the smallest partition into which it will fit. This is very simple to implement, but memory is wasted if a process doesn't fill its partition, and larger processes can't necessarily be run at all. Variable size partitions are most effective if the expected process sizes are already known.

In early systems, if a process was too large to fit in any partition, *overlays* could be used. This meant that not all of the code would be loaded into memory, and a subroutine in the program would load in code from storage when it was needed, overwriting another part of the same program. The same could be done with data, if the data held in memory was written to storage first. This technique was difficult to implement.

Processes need to be put into a contiguous area of memory because it would be complicated for the OS to remember which areas of memory are owned by which processes, and code can't be split up because instructions must be in sequence for the program counter to work correctly. However, this can all be solved using *virtual memory*.

Dynamic partitioning (still a type of static allocation) is more complicated to implement than partitioning, and allows each process to state how much memory it will need when it starts. The OS will allocate that much memory to that process. Memory can be allocated sequentially to processes from the bottom (where the kernel lives) to the top.
![](http://i.gyazo.com/71b5a8211d634b27dfa212047e567f1a.png)
The problem with this is that when a process finishes, it will leave a hole where it was. Even if there is enough memory to run a new process, unless the memory is contiguous then the new process can't be started. This problem is called *fragmentation*. The more processes come and go, the worse the fragmentation becomes.

The kernel keeps a list of free blocks of memory, called the *freelist*. When a block is freed, it is added to the block. When two adjecent blocks are freed, they are coalesced into one block. When a new process starts, the freelist is searched for a space to put it. There are several strategies for choosing a block in the freelist:
- Best fit: the smallest available free chunk is used. This is slow because the whole list must be searched and the fragments this leaves are small, increasing fragmentation.
- First fit: the first free chunk big enough is used. This is initially fast, and leaves bigger and more useful fragments, but tends to fragment the start of memory meaning the search takes longer as time goes on.
- Worst fit: the largest free chunk is used. This leaves larger fragments that are more useful, and is faster than best fit because there are fewer fragments to search.
- Next fit: the next space after the last one allocated is used. This is fast and spreads small fragments through memory.
There are many other algorithms, and despite virtual memory not having these problems, some components (eg GPUs) still need contiguous physical memory so freelists are still maintained.

If a big enough space can't be found, the OS runs the *garbage collection*. This is stops all processes from being scheduled, and defragments memory by moving all processes down to close up fragments. Garbage collection is not often used in OSs because it is very expensive and would make a real-time or interactive system difficult to use, because all processes must pause while it happens.

Garbage collection also relies on processes being relocatable, meaning they must only use relative JUMP operations rather than absolute memory locations. This is a reasonable assumption in modern OSs, but any processes that break it will not work after garbage collection has run.

If a suitable free space can't be found even after garbage collection, there are several options:
- Don't admit the new process
- Kill an existing process. This means any work it did will be lost, and should be avoided
- Preemption of memory belonging to another process
- Swapping

######Swapping

Swapping is where a process is selected by the OS and copied from memory to disk. Typically, a blocked process is chosen to minimise impact on the system. When the swapped process is scheduled again, it must be copied back into memory again, which might require swapping something else out.

The difference between swapping and overlays is that swapping is done by the OS transparently to the process and programmer, where overlays were controlled by the programmer. Swapping also applies to multiple processes where overlays applied to multiple sections of the same process (though types of swapping can do this too).

The task of choosing which process to swap isn't easy. An I/O intensive process won't be scheduled for a long time, but when it is scheduled again it must respond very quickly. A CPU intensive process benefits from being scheduled often but is not so sensitive to a delay through being swapped.

Swapping is helped by *paging*. Fragments and processes can be irregular sizes, so copying them from and to disk can't be optimised. Paging splits memory into small contiguous chunks, typically 4096 bytes. The hardware is then optimised to copy a whole page at a time, and processes can't own part of a page.

######Virtual memory

Addresses can be *virtual* or *physical*. A physical address is the numbering of the actual bytes in memory, but each process sees only virtual addresses, which are the bytes it owns in memory but renumbered to start from zero. The system can translate between virtual and physical addresses on the fly using *page tables*.

A per-process page table contains mappings from virtual to physical address for that process. Each page in the process's virtual address space matches with a page in the physical memory. This means different processes can use the same virtual addresses but have them correspond to different physical addresses. It also means physical memory doesn't have to be contiguous any more, because the virtual memory is contiguous. This also increases security, because not only are processes not allowed to access each other's memory, they now physically can't attempt to.

These tables are stored in memory as part of the process control block. This would mean that every time an instruction was executed or data read or written to memory, there would be another memory read first to find the mapping. This isn't feasible, so a piece of hardware called the *translation lookaside buffer* (TLB) is used. This is part of the memory management unit.

The TLB keeps a copy of a small subset of the mappings from the page table of the currently running process and can translate them very quickly. The TLB is small (only a few hundred entries) because the memory used is so expensive.

When the CPU sends an address to the TLB it looks it up in its table. If it is present, this is a *TLB hit*. If it isn't, this is a *TLB miss* and the mapping must be fetched from memory. Two techniques can be used for this. A *page walk* is used in a hardware-managed TLB. This is where the TLB itself looks up the translation in memory, installs it into the table, and carries on. The OS is not involved with or even aware of the miss.

The second technique, in a software-managed TLB, is to raise a TLB miss interrupt when a TLB miss occurs. The OS then performs the page walk.

If the process isn't currently using the page it's requesting, or the page was swapped, the page table won't have a mapping for that page. A *page fault* interrupt will be raised and the OS will allocate a physical page and write the relevant mapping to the TLB and page table. The OS could alternatively choose not to allocate a page, and send a segmentation violation signal to the process.

*Minor page fault* refers to a TLB miss, and *major page fault* refers to a page fault.

The speed of translation relies on the TLB maintaining a good proportion of currently used addresses, to minimise page faults and TLB misses. A well-written program will tend to use the same addresses a lot, and these will be loaded into the TLB for fast translation.

If a page has been swapped out to disk, a page fault will be raised and the page will have to be copied back into memory from disk. This is a very slow operation.

If there is a TLB miss and the TLB table is full, the OS will typically remove the least recently used entry because pages that haven't been touched in a long time are often not needed in the near future. This is called *temporal locality*. The TLB therefore has to keep track of when each page is used.

There are many strategies for choosing which page should be swapped from memory to disk:
- Random: picks a random page. This is simple and surprisingly effective
- First in first out: this is poor because the pages that have been around a long time are often frequently used
- Least recently used: good, but needs hardware support to keep track of when each page is used
- Least frequently used: poor, because pages just brought in will have a low use count

The first time a page is touched by a process a page fault will be raised and the OS will allocate a new physical page. It doesn't matter which physical page is used; the first in the free list is as good as any other. This is the main advantage of using pages.

*Lazy page allocation* is a fairly efficient strategy. This only allocates pages when they are touched, rather than when they are requested. If a process requests two pages and then only touches one of them, rather than the other page being taken off the freelist but unused, the pages will only be allocated when the process makes a request for data in that page.

Problems with TLBs are that they have a small capacity, and they rely on temporal locality. These are generally not big problems. The biggest problem with TLBs is when the OS does a context switch, where the running process ends its time slice and another one is started, the TLB must be flushed and repopulated. This means that at the start of each time slice, there will be lots of TLB misses and page faults.

More sophisticated TLBs have an *address space number* (ASN) tag on each entry in the table. This relates each entry to a process. Mappings don't need to be flushed, and when the TLB runs out of space the mappings relating to old processes can be evicted first.

When a process tries to read, write or execute a page which it doesn't have permission to, the OS sends a segmentation violation signal to the process. This is useful when processes can share memory. The TLB makes memory sharing easy, because different virtual addresses can be mapped to the same physical addresses.

This use of shared memory allows for *shared libraries*. Many programs have shared functionality such as writing to files, so rather than reimplementing all of this in every program, the program simply refers to the relevant library. These are not part of the OS, but provide interaction with it.
![](http://gyazo.com/c8c85f37d9b5445bdc9a28c9b43c4560.png)
Each program using the library has a virtual address to it, and each of these is mapped to the same physical address so the library only needs to be in memory once. This reduces page faults as well as reducing memory usage.

A similar trick can be used for data. Different processes can share the same data as long as they don't try to update it, and data that processes do want to update can be put in pages with the *copy-on-write* flag set.

Copy-on-write shares data until one process tries to modify it. When it is modified, a page fault is raised and the OS makes a physical copy of that page with the modifications. It updates the page table for the modifying process. The other processes still see the old unmodified data. This again reduces memory usage and page faults. It is more complex to implement but overall is more efficient.

Another trick is to keep a page full of zeros. If a process asks for a block of zeroed memory, the OS can give it a list of virtual addresses pointing to the same physical page of zeros. When the process tries to modify it, the OS does a copy-on-write. Only pages which are actually used get allocated.

*Memory mapping* is where parts of the virtual address space correspond to devices other than memory. For instance, a process could write to the screen or a file as easily as writing to memory, with the conversion performed by the OS transparently to the process. This makes programming simpler because the programmer doesn't have to worry about how to write to the hardware, it simply treats it like memory and lets the OS do the implementation.

There are two problems with the speed of memory. The first is the clock speed, although this is not as pronounced as it was once. Processors run faster than memory so even if they constantly read then they'll still have empty cycles. The other is latency, where there is a delay between requesting a value and it coming back. This delay can be dozens of clock cycles.

The slow speed can be overcome by having multiple channels to memory. Latency needs a different solution, namely *registers*. A register is a very fast on-processor memory location, and as much processing as possible is done only storing the values in registers and writing them back to memory at the end of a calculation. They are very expensive and we can only afford a few hundred bytes, but this idea can be extended.

The *cache* is a relatively small amount of fast memory between the CPU and main memory. It contains a copy of some of the data in memory. When the CPU reads from memory, the cache is checked first. If the value is present, this is a *cache hit*, and the value is returned quickly. If not, this is a *cache miss*, and the value is fetched from main memory and sent to the CPU and also stored in the cache.

There are many similarities to paging. We have to decide what gets evicted when the cache is full, hits are fast and misses are slow, and complex hardware support is required.

There are also similarities to the pages themselves. A *cache line* is a block of contiguous memory that is read and written as a whole rather than individual bytes. These reduce the complexity of the lookup system, and is effective because of locality: nearby bytes are likely to be needed soon, and they are already in the cache.

Writing to memory also goes via the cache, using either a *write-through cache* or a *write-back cache*.
- Write-through cache writes a value to main memory as soon as the CPU writes it to the cache
- Write-back cache writes to main memory only when it is convenient, or when the line is evicted from cache

Cache memory is very expensive, so the most effective way of extending the cache is to use a *multi-level cache*. In this system, the cache has a cache: there is a second larger and slower cache between the first one and main memory known as the L2 cache. Modern processors extend this to an L3 cache as well. Programs written to be sensitive to cache behaviour are much faster.

Caching, therefore, happens at many levels, from fastest to slowest:
- Registers (in the CPU)
- L1 cache (in the CPU)
- L2 cache
- L3 cache
- Main memory
- In a sense, main memory is a cache for disk because programs are stored on disk and swapped to memory
- Disks can act as caches for offline storage such as tapes

All of this assumes locality. Most programs tend to do this naturally, because the data recently accessed is normally the data that is changed and written. It is easy to write programs for which this isn't true.

There are two types of locality: temporal, meaning that recently accessed data is likely to be accessed again soon, and spacial, meaning that locations near a recently accessed location are likely to be accessed soon.

Because data and code are accessed in different ways, some architectures have two separate caches for code and data. This is called a *Harvard architecture*. Modern Harvard chips have two L1 caches and unified main memory. This can be a problem for dynamic languages, because they create data which must be evaluated as code, meaning it has to first pass through main memory and into the other cache, which is a slow operation.

Memory access and 
