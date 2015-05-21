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
