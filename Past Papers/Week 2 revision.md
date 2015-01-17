1a) Processor executes instructions sent to it by the control unit
Control unit gets instructions from the store and sends them to the processor
Store contains programs and data in cells
Input devices feed input to the computer from the physical world
Output devices allow the computer to give output to the physical world
b) In the Harvard architecture, separate stores are used for programs and data. This helps avoid the von Neumann bottleneck but is less efficient, because different memories have specific jobs so aren't as flexible.

2) The von Neumann bottleneck is a problem caused by the fact that the CPU and memory both operate faster than the bus connecting them can. The CPU therefore wastes time waiting for data from memory. Its impact can be reduced by providing the CPU with faster memory locations like caches, and by using alternative architectures such as Harvard which do not need to get their programs and data from the same store.

3) Flynn's taxonomy describes parallel architectures.
Single Instruction Single Data: not parallel, one processor performs one operation at a time on one stream of data.
Single Instruction Multiple Data: multiple processors perform the same instruction simultaneously on different streams of data.
Multiple Instruction Single Data: multiple processors perform different instructions simultaneously on copies of one stream of data.
Multiple Instruction Multiple Data: multiple processors perform different instructions simultaneously on different streams of data.

4a) SIMD because the same operation is performed on different pixels
b) MISD because the same inputs are fed to different processors so each can use a different method

5) Shared storage: One pool of memory for all processors. Fast, but can cause cache coherence problem if two processors try to edit the same piece of data.
Distributed storage: One store for each processor. To request information from another processor's store, a complex and slow message-passing system must be used.
