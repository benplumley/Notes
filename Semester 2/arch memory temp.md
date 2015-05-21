###Memory

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

Swapping is where a process is selected by the OS and copied from memory to disk. Typically, a blocked process is chosen to minimise impact on the system. When the swapped process is scheduled again, it must be copied back into memory again, which might require swapping something else out.

The difference between swapping and overlays is that swapping is done by the OS transparently to the process and programmer, where overlays were controlled by the programmer. Swapping also applies to multiple processes where overlays applied to multiple sections of the same process (though types of swapping can do this too).

The task of choosing which process to swap isn't easy. An I/O intensive process won't be scheduled for a long time, but when it is scheduled again it must respond very quickly. A CPU intensive process benefits from being scheduled often but is not so sensitive to a delay through being swapped.

Swapping is helped by *paging*. Fragments and processes can be irregular sizes, so copying them from and to disk can't be optimised. Paging splits memory into small contiguous chunks, typically 4096 bytes. The hardware is then optimised to copy a whole page at a time, and processes can't own part of a page.
