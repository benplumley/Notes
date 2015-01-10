#CM10194 - Computer Systems Architecture I
##Dr Fabio Nemetz <small>Labs: Daniela, Christina, Saeid, Gideon</small>

**Analogue Computing**  
Analogue variables are *continuously variable*, and have precisely exact values. However, when their values are read, either by a human or the analogue computer system, they lose their precision and thus their accuracy.

**Digital Computing**  
Digital computers use *discrete* data values to represent variables. This means they are imprecise (because a temperature recorded as 23.1C might actually be 23.098659...C) but their values can be read with absolute precision.

**First Generation of Digital Computers**  
The first generation of computers used vacuum tubes (valves) and were around in the 1940s. Examples include Bletchley Park's *Colossus* and von Neumann's *ENIAC*.

**Second Generation**  
The second generation used a relatively new invention, the *transistor*. This allowed a small current to control the flow of a larger one. Compared with valves, transistors were smaller, more durable with a longer lifespan, used less power and produced less heat. They were also cheaper than their glass counterparts, meaning computers could be smaller, cheaper to make and easier to maintain. Among the first commercial computers to use them was IBM's *608* from 1957.

**Third Generation**  
The third generation improved on the transistor by putting many of them onto the same piece of silicon. This was called the *integrated circuit*, or chip. The first chips, in 1961, had only a few tens or hundreds of transistors per chip.

**Fourth Generation**  
The fourth generation was the evolution of the chip - called *Large Scale Integration*, or LSI, an integrated circuit in the 1970s might have had tens of thousands of transistors on it.

**Fifth Generation**  
This is the current generation of computers. It began in the mid 1980s and is known as *Very Large Scale Integration*, or VLSI. A VLSI chip can have several billion transistors.

**Von Neumann Architecture**  
This is what almost all commercial laptop and desktop computers use today. Named after its creator, John von Neumann, this architecture is based around the idea that a computer inherently contains five components:  
- The *Arithmetic and Logic Unit*, or ALU  
- The Control Unit, which sends instructions (operators) and data (operands) to the ALU  
- The data store, which contains both data and instructions. In this context, it refers to the RAM  
- The input devices (mouse, keyboard)  
- The output devices (screen, printer)

Crucial to this architecture is that the same data store is used for the data as is used for the instructions. This follows from the principle that instructions can be represented as data, and is known as the *stored program concept*. The CPU is made up of the ALU and its Control Unit.

There are drawbacks to the Von Neumann architecture. Because the CPU can process data faster than it can be written to the data store, a bottleneck can form between the CPU and memory. This is exacerbated by the processing of small files, where the ratio of data to be processed to 'overhead' (metadata, address locations etc) is low. This has become more of a problem as CPU speed has increased at a greater rate than the speed at which memory can be written to. It can be alleviated through the use of caches, which are small fast memory locations near the processor.

**Harvard Architecture**  
The main difference between the Von Neumann architecture and the Harvard architecture is the data store. The Harvard architecture uses two separate data stores; one for data and the other for programs. Embedded devices, including members of the Arduino line, use this architecture.

**Parallel Architectures**  
There are a number of solutions to the Von Neumann bottleneck. These include using an alternative architecture (eg Harvard), the use of distributed storage, caching and internal registers.

A *cache* is a small memory location which is faster than main memory, and duplicates some of the information stored in main memory so that it can be accessed more quickly. It is split into levels. *L1* cache is the fastest and smallest cache, and is located on the CPU itself. *L2* cache is bigger but slower, located near but not on the CPU. More modern processors can have more levels of cache, which are progressively larger and slower, and further from the CPU.

A *register* is a memory location used to store the results of ongoing calculations. It is smaller and faster than the L1 cache.

*Parallelism* is a processor carrying out multiple operations simultaneously by having more than one ALU. This is known as a multiprocessor. The behaviour of multiprocessors and the programs they run is harder to understand, control and predict. Parallelism can be broken down into task level parallelism and data level parallelism. Task level parallelism can either use a single instruction stream or multiple instruction streams, and data level parallelism can either use one data stream or multiple data streams. Therefore, the four possibilities are:  
- Single Instruction, Single Data (SISD): Performs one instruction at a time. This isn't parallel.  
- Single Instruction, Multiple Data (SIMD): Performs the same operation simultaneously on multiple pieces of data, for example to change the brightness of every pixel in a photo. This is the architecture used in modern GPUs.  
- Multiple Instruction, Single Data (MISD): Performs different operations simultaneously on the same piece of data. This has uses in fault tolerant computing, where lots of methods are used on the same data to ensure they have consensus.  
- Multiple Instruction, Multiple Data (MIMD): Performs different instructions simultaneously on different pieces of data. The actions of one ALU have no bearing on the actions of the others.

There are also two types of *memory architecture* in a multiprocessor. One, *shared memory*, uses a single pool of memory addresses that can be accessed with equal speed by every CPU. This is efficient as little space is wasted, but bottlenecks can form and if two CPUs change the same piece of data, something known as a *cache coherence problem* is caused. Shared memory also doesn't scale well.

*Distributed memory* is a system where each CPU has its own pool of memory which only it can access. This isn't as space-efficient, and in order to request data stored in another processor's memory, a relatively slow message-passing system is required. Also, the process of splitting and distributing a task to separate CPUs and then reassembling their computed outputs from separate memory pools is a non-trivial problem.

Compromises between the two architectures exist: *virtual shared memory*, where the action of requesting another processor's data is transparent to the CPU, and *non-uniform memory access*, where a shared pool is structured in such a way that each processor has a preference for a certain section of the pool.

The dominant form of architecture in commercially available CPUs is a MIMD processor with shared memory.

**Amdahl's Law**  
Amdahl's Law describes the limits to the benefit provided by parallelisation. It says that, if proportion *p* of a task can be done in parallel, the speedup provided by a computer with *N* processors is:  
1 / ((1 - p) + (p / N))

For instance, a task of which 90% can be parallelised, given to a 4 core processor, will be completed 3.08 times faster than when given to a single core processor. This formula has a limit as N tends to infinity. The task which is 90% parallel can be done at most ten times faster than on a single core. The limit is 1 / (1 - p).

**Data Representation**  
Computers store many forms of information using only a two-state system. By setting or unsetting a series of bits, or flipping a bit on a magnetic drive, the computer can represent any piece of data of any data type. Integers, characters, addresses and instructions are all stored together on the same disk with nothing to differentiate one type from any other apart from the context in which that memory location will be referred to.

The binary system is a form of representational numeration system, ie a series of symbols that represent quantities. A good coding system:  
- has an easy-to-remember alphabet. The alphabet of a system is the numerals that make it up, eg 0 and 1 in binary, 0-9 in decimal and 0-F in hexadecimal.  
- is unambiguous. One pattern of numerals must represent only one number, and each number must be represented.  
- is economical in use. This depends on the context - it is beneficial to humans to have ten different symbols and relatively short strings of numerals, whereas a computer operates more efficiently by having only two possible symbols (which can then be represented as voltage or lack of voltage) and relatively long strings of numerals.  
- represents a numerical quantity.  
- can be easily manipulated, for instance to perform arithmetic.

In the decimal system, we represent digits larger than 9 by combining groups of digits together. Each digit's value depends on its numeral and its position in the number (tens column, units column etc). This is called a positional notation. A digit's value is calculated by multiplying its numeral by the base to the power of its position. Hence  
352 = 3*10^2 + 5*10^1 + 2*10^0

The binary system works in the same way, only it uses 2 as the base rather than 10. So the number  
0b101110 = 1*2^5 + 0*2^4 + 1*2^3 + 1*2^2 + 1*2^1 + 0*2^0  
This is also the method for converting a binary number into a decimal one. Columns containing 1 add their positional value (2^position) to the answer; columns containing 0 add nothing. Hence  
0b101101001 = 256 + 64 + 32 + 8 + 1 = 361  
Converting a decimal number to binary follows much the same process in reverse. The largest power of 2 is subtracted from the number, and a 1 is put into its column in the result. This is repeated until the decimal number left is zero. To convert 165 to binary  
165 - 128 = 37	so the answer contains a 1 in the 128 column  
37 - 32 = 5			so a 1 in the 32 column  
5 - 4 = 1				so a 1 in the 4 column  
1 - 1 = 0				so a 1 in the 1 column, and finished because we reached zero.  
Therefore 165 = 0b10100101, where columns that were not part of the subtraction contain 0.

A few more conditions must be met by a numeration system. These are:  
- There must be as many digit symbols as the base.  
- Place values increase from left to right; the value of each place is equal to the base to the power of the position  
- There is an agreed starting point (units) denoted by a point

These systems can be extended to the right of the point to represent non-integer numbers. Putting a number to the right of the point means it has a negative position, so the base is put to a negative power. A binary number can be written more succinctly in hexadecimal by converting every series of four bits into a single hexadecimal digit.

**Data Storage**  
The basic element of digital storage, is the binary digit, or bit. This is a two-state device, represented in a computer either by a presence or absence of charge of polarity of magnetisation. These bits are grouped into sequences called cells. A typical cell size is 8 bits; this is a byte. Other cell sizes are also sometimes used.

The store (main memory, RAM) is a large collection of addressable cells. Individual cells can be referred to by their address, and they are the smallest addressable unit in the store - you can't directly address a single bit. The states of the bits in each cell make up its contents. Each cell has a unique address, typically starting at 0 and counting up.

Two types of memory access are Random Access (in RAM) and Sequential Access (in a hard drive). With Random Access Memory, the time taken to access a cell does not depend on its address. With Sequential Access Memory, the time taken to access each cell depends on the distance between it and the cell previously accessed, typically because a mechanical read-write head has to physically move a distance to find the next cell.

The contents of a cell, a bit pattern, is agnostic to data type - it is impossible to tell what type of data a cell holds without knowing the context in which it will be accessed. As addresses themselves are data, cells can hold addresses of other cells.

The *address space* of a computer refers to the number of bits on its address bus, and hence the number of different locations it can access. For instance, the address bus on a 32-bit computer contains 32 wires, and can represent 2^32 addresses. These addresses must be split between RAM, I/O devices, networked computers etc. The processor's address space must be greater than or equal to the operating system's, which must be greater than or equal to the application's. For this reason, a 32 bit app can run on a 64 bit processor but not vice versa.

By doing a direct translation from a decimal number to a binary one, we can store a number between 0 and 255 in one byte. However, this is not the only way of using bytes to represent unsigned integers. Other methods include Binary-coded Decimal (BCD) which assigns a 4-bit pattern to each decimal digit. Early decimal computers used this encoding. Binary-coded sexagesimal uses 6 bits per digit to store a number between 0 and 59, and can therefore be used to represent time. Gray codes are another system, in which two successive values differ only in one bit.

**Signed Integers**  
We can use *sign and magnitude* to store a number between -2^n and 2^n in a cell of n+1 bits. The first bit represents the number's sign (eg numbers starting with 0 are positive, numbers starting with 1 are negative) and the remaining bits represent the magnitude of the number.

The advantages of this method is that it is easy for humans to read it, and symmetrical about zero. However, as there are positive and negative values of zero, only 255 values can be stored instead of 256 in a byte. It also makes arithmetic more complicated than it needs to be, because there must be a case in the processor for each combination of signs.

An improvement over sign and magnitude representation is *1's Complement*. Positive integers are still represented by a number with a leading zero, but to get a negative number, all the bits are flipped from its positive counterpart. The advantage of this is that arithmetic is much simpler, but there are still two representations of zero.

The method used by modern computers is *2's Complement*. In this representation, the MSB represents the negative of its position's value (in a byte, -128) and the remaining bits represent an unsigned integer. For instance, 0b10110100 is -128 + 32 + 16 + 4 = -76. This method's advantage is that there is now only one representation of zero (0b00000000). All negative numbers have a 1 in the MSB, and all positive numbers have a zero. However, the number line is no longer symmetrical about zero, and this form can be hard for humans to read.

Another big advantage of 2's Complement is that arithmetic can be carried out in a single stage, without having to check the sign of the numbers we perform the calculation on. Addition works exactly as it did with unsigned integers, and now subtraction can also be performed by adding a positive and a negative number together.

**Text Characters**  
To store a character, we assign it a unique bit pattern. All of the symbols in the Western alphabet (upper and lower case characters, numbers and punctuation) can be represented in one byte. A string of characters is stored in a series of bytes. The ASCII scheme is one of the most common character encoding schemes, and uses 7 bits to store a character. UNICODE uses 32 bits, therefore can be used to store characters from any language.

**Real Numbers**  
An ideal encoding of real numbers would be precise and unambiguous. However, the decimal system is unable to achieve this, needing to fall back onto letters representing numbers (e and pi) and fractions. The binary floating point system is no different. It uses the binary equivalent of scientific notation to approximate the values of real numbers. This notation uses a *mantissa*, *base* and *exponent*.

Advantages of scientific notation are that they are easy to understand, generate and manipulate, they are compact in their representation, they can represent numbers of widely varying magnitude, and they are accurate up to the level of precision they specify.

Disadvantages are that the number is inherently an approximation, rounding errors can occur, and using different formats to represent the same number can give different answers in a calculation. Because of the nature of real numbers, each floating point number represents an infinite number of real numbers.

In normalised scientific notation, both the mantissa and exponent are signed. The mantissa must be between 1 and the base.

As the size of the mantissa is fixed, we can only give approximate values of numbers which have a greater number of significant digits than the size of the mantissa. Some of the accuracy of the original number will be lost if the mantissa is smaller than the number it is representing. The number of bits given to the mantissa affects the accuracy of the representable numbers, and the number of bits given to the exponent affects the magnitude.

The IEEE has a standard for how floating point numbers are stored in memory. The first bit holds the sign of the mantissa. The next 8 bits holds the exponent plus a bias of 127 which must be subtracted to calculate the value of the exponent. The next 23 bits are the 24-bit mantissa, where the first bit is always 1 so doesn't need to be stored. The binary point is therefore to the left of the first bit stored in the mantissa.

Special cases are an exponent of zero (representing zero) and an exponent of 255 (representing infinity).

To add two floating-point numbers, the smaller one is de-normalised so its exponent is equal to the other exponent, the mantissae are added, and the result is re-normalised. To multiply, the mantissae are multiplied, the exponents are added and the result is re-normalised.

Double precision floating point numbers use 64 bits instead of 32. The exponent is 11 bits and the mantissa is 52 bits.

**Instructions**  
As well as data, instructions are held in the store of a von Neumann computer. Instructions consist of an operation and zero or more operands. The design of an instruction set will try to maximise the amount that can be done while minimising the amount of space taken up by each instruction.

In order to provide a meaningful number of operations, instructions typically take up more than one byte. The number of bytes taken up depends on the instruction set being used and the particular instruction. In the x86 architecture, instructions typically take up 2-4 bytes, but can take up as few as one or as many as 15. Typically, an instruction might use 2 bytes for the operation and 2 or 4 bytes for each operand.

Because processors are so much faster than memory, registers and caches are used to limit the effects of the von Neumann bottleneck. Registers consist of arrays of bits, and contain the data that is currently being processed by the ALU. The control unit also has registers which store program information.

Assuming there is only one data register in the CPU, that register can always be used as an operand of a two-operand instruction such as addition. The instruction does not then need to encode this operand each time, because it can be assumed that the operand given is to be added to the one already in the processor. In this case, addition of two numbers is now a sequence of instructions: the first loads the first operand to the register, and the second adds the second operand to the first. The third stores the result back into memory.

In practice, processors have more than one data register, so it must be specified in the instruction which register is being referred to. This bit pattern can fit in the bytes assigned to the operation. These are known as *one-and-a-half address codes*. An operation taking no operands (but optionally a register) is known as a *zero address code*. An instruction taking two addresses in memory as operands is known as a *two address code*.

A program can be thought of as an ordered sequence of instructions. To progress through a program, we perform its instructions in order by stepping through and executing store addresses in sequence. To keep track of where the program is currently executing, we add registers to the control unit. These are not directly accessible to the programmer, even in assembly language.

The *Program Counter (PC)* holds the address of the next instruction to be executed. The *Instruction Register* holds the contents of the current instruction being executed. The *Memory Address Register (MA)* holds the address that is being accessed and the *Memory Buffer Register (MB)* holds the data held at that location after a read, or the data to be written to that location. The control unit uses these registers to get instructions from the store and send them to the processor. By sending a read command on the control bus and the contents of the MA on the address bus, the store responds by sending the contents of the address in the MA along the data bus to the MB. The write operation is similar, only the contents of the MB are sent on the data bus at the same time as the contents of the MA are sent on the address bus.

**The Instruction Cycle**  
The instruction (or fetch-execute) cycle is a series of steps that are iterated through each time an instruction is performed:  
1) The instruction is fetched from the store to the control unit, and the PC is incremented  
2) The instruction is interpreted to decide what the operation is and what operands are needed  
3) The operands are fetched from the store to the ALU  
4) The operation is executed on the operands fetched  
Step 1 is the *fetch phase*; steps 2-4 are the *execute phase*. The fetch phase is the same for all instructions but the execute phase varies depending on the operation.

The fetch phase can be broken down into stages.  
1) The contents of the PC are placed into the MA, to be sent to the store along with a read command on the control bus  
2) The contents of the store at the address in the MA are sent along the data bus to the MB  
3) The contents of the MB are placed in the IR to be decoded  
4) The PC is incremented  
Note that the amount the PC is incremented by depends on the number of bytes taken by the instruction just read. After being incremented, it will point at the next instruction to be executed.

**Addressing Modes**  
Operands can be addressed in ways other than storing the address of the value to be used as an operand. These are, in order of speed:  
- Immediate. The number specified after the operation is the number used as the operand  
- Direct. The number after the operation is the address of the operand  
- Indirect. The number after the operation is the address of a cell containing the address of the operand  
Other addressing modes can be used, but these three are the most common.

**Instruction Sets**  
The two major groups of instruction sets are Complex Instruction Set Computing (CISC) and Reduced Instruction Set Computing (RISC). CISC instructions are:  
- more powerful. One instruction can describe a complicated operation  
- harder to decode. Because there are more instructions, decoding each one takes longer  
- able to access memory directly from a non-memory related instruction. For instance, an addition instruction could first pull the two values to be added from memory  

RISC instructions, in contrast, are:  
- simpler. One instruction only does a simple task, and instructions must be combined to achieve the functionality of a single CISC instruction  
- easier to decode. Fewer possible instructions means they are fast to decode  
- only able to refer to registers. Separate instructions must be used to first load these registers with the desired values  

The CISC instruction sets are used in architectures such as x86. RISC instruction sets are used in mobile and embedded architectures such as ARM.

**Control Instructions**  
There are some instructions able to alter the contents of the program counter. These are known as *control instructions*. They are the *unconditional branch*, or *jump*, and the *conditional branch*, or *jump if*. The jump command simply replaces the contents of the PC with its operand, so that the program jumps from wherever it is currently executing to the number specified by the jump command. The jump if command does the same, but only if a specified condition is met. This condition can be a comparison, for example to jump if two registers are equal or a specific register contains zero, or a test, for example if the last arithmetic operation resulted in overflow (meaning the overflow flag was set).

These control instructions are what enable the use of programming concepts such as decisions, loops and functions. Without them, all programs would have to execute one line at a time from top to bottom. When a jump happens, the program executes in the new location until it reaches a return statement, at which point it returns to wherever it was executing before the jump was called. In order for the processor to remember where this was, particularly considering that the code could jump any number of times before returning, we must introduce the concept of a stack.

The *stack* is an area in memory that uses the Last In First Out principle (similar to a stack of plates, where they can only be added or removed from the top). A register called the *Stack Pointer (SP)* is used to store the address of the current top of the stack. To push a value, this register is decremented (because stacks typically store from high addresses to low addresses) and the value is stored at this address. To pop a value, the store value at the address in the stack pointer is retrieved and the SP is incremented.

This structure extends easily to the task of storing subroutines as jump commands are given. Before the processor jumps, the current location is pushed to the stack along with the values of all the registers - this is known as the *stack frame*. When the subroutine returns, the top element from the stack is popped, loading the values of all registers to what they were before the jump. This includes the PC, so the program goes back to where it was before the jump. This means subroutine calls can be nested to any depth, provided we have enough space on the stack to store each stack frame.

**Pipelining**  
As the ALU, control unit and memory can all be working at the same time, performing the fetch-execute cycle in sequence wastes resources. While the processor is waiting for the memory to return a value, it is doing nothing. For this reason, we use *instruction level parallelism*, specifically *pipelining*. There are five element to the cycle:  
1) Fetch instruction  
2) Decode  
3) Fetch operands  
4) Execute operation on operands  
5) Store result  
Pipelining is the process of starting the next instruction at step 2 of the current instruction and so on with the next one until we have 5 concurrent instructions, one at each stage of the cycle.

This is better than performing instructions strictly in sequence, but it's not ideal because instructions aren't always stored in exact order of operation. For instance, if the first instruction is a jump, the next three instructions will have been fetched by the time the jump reaches the execute phase, at which point the three instructions must be discarded and the process started again. There are a number of ways of limiting the impact of this problem:  
- Avoid branches in code. Not very practical in any programs of meaningful size  
- Predictive decoding. Based on heuristic analysis, predict where the jumps will occur and pipeline the most likely sequence of events  
- Multiple pipelines. Keep a separate pipeline for each possible branch, and discard all but the correct one when it's reached  

It also falls down when one instruction depends on the result of the one immediately before it, known as an *instruction conflict*. For instance, to add two numbers and then store the result in memory, the operands for the store command are fetched before the result is stored, meaning if the processor doesn't wait for the dependency to resolve, the value stored will be an outdated one.

*Load delays* also slow the pipeline down, because the fetch stage is slower than the decode and execute stages.

**Superscalar Architectures**  
Another form of instruction level parallelism is *superscalar architectures*. This technique involves noticing when two instructions do not depend on one another and executing them completely in parallel (ie stage 1 of the first is done at the same time as stage 1 of the second). This is achievable because within the CPU are different components which have different tasks, such as to shift bits, multiply numbers etc. Two or more of these components can be used completely independently, so if two instructions use different processor components, then they can be executed exactly in parallel.

An architecture may be pipelined, superscalar, both or neither.

**Input/Output**  
The fourth and fifth boxes in the von Neumann model are *Input* and *Output*. Any transfer of information beyond the CPU and main memory is I/O, including storage to a hard drive. It is the job of the architecture to specify how information will be sent and received consistently depsite the large variation in purpose and capability. The architecture must also be able to communicate with devices which have not yet been invented.

Communication must function regardless of operating speed of the I/O device. From fastest to slowest, devices can be  
- electronic, such as other networked computers or flash storage  
- electromechanical, such as magnetic disks and printers  
- human, such as mice and keyboards.  
They also vary in their ability to be controlled by the CPU:  
- Under complete control of the CPU, such as graphics in some systems  
- Not under CPU control, such as a keyboard  
- Both, such as a network which both responds to and makes requests of the CPU  

In order to communicate with I/O devices, the control unit is connected to an *I/O control unit*. This sends an instruction to an I/O device, which can then start to read from or write to the data register in the CPU. The instruction sent by the I/O control unit encodes the *operation code*, *direction of transfer* and the device's address. This is enough to tell the device to send or receive a particular piece of data. This information is sent along an I/O address bus to which all I/O devices are connected, which is why it is necessary to specify the address of the device. Devices respond by placing their information on the I/O data bus.

The advantages of giving all I/O devices a shared bus is that it is simple and flexible, and can be extended for more devices. The disadvantages are that it is expensive to add a bus to a computer, and that two devices could contend for use of the bus. This is resolved by designing programs in a way that only one device at a time accesses the bus, or adding a piece of hardware to the system to limit the bus to one user at a time.

**Memory-mapped I/O**  
Rather than creating separate buses for I/O, it is common for I/O devices to occupy some of the locations addressable on the architecture's existing buses. This is known as *memory-mapping* of I/O devices. Address, data and control buses are all connected to each I/O device and each one is referred to as a location in memory. No special I/O instructions are needed in the instruction set, as we can load and store data in I/O devices as if we were loading and storing it in main memory.

The main advantages of memory-mapping are that it simplifies use of I/O devices, and reduces the size of the instruction set. The disadvantages are that it uses address space which cannot then be used for storage (which is much less of a problem in 64 bit architectures), it puts I/O devices in contention with the store for the bus, and it can be harder to understand programs written in low-level languages because main memory and I/O devices are referred to in the same way.

**Co-ordinating I/O devices and CPU**  
In order to let the CPU know when an I/O device is ready, each is assigned a register containing (at least) a one-bit flag representing the state of the corresponding device. When a transfer is started, the flag is unset, and when the transfer completes the flag is set to let the CPU know that the device is ready to recieve another transfer. The CPU can test the flag at any time, which is a much faster operation than sending a status request to the I/O device.

The problem with writing code that refers to I/O devices is that their moving parts make them many orders of magnitude slower to operate than the CPU. If the code had to wait for an electromechanical I/O device to be ready before it could continue, the entire program might be forced to operate at the speed of a mechanical arm or print head. This method of operation is known as the *busy-wait strategy*. The CPU tests the device flag, and the device is ready, the CPU will begin the transfer. If the device is not ready, the CPU will repeatedly test the flag until it becomes ready. Until the mechanical device is ready, the CPU does no useful work, making this a very inefficient strategy. However, the CPU will know the device is ready as soon as the flag is set, so no time is wasted after the flag is set.

An alternative strategy is *polling*. The CPU tests the device flag, and if it is unset, does another useful task for a set amount of time, and then tests again. It repeats this until the device becomes ready. This wastes fewer cycles than busy-wait, but cycles are still wasted testing the flag and if the flag is polled just before being set, the CPU must wait a relatively long time doing unrelated work before testing the flag again.

Both of these methods are flawed, so a method is needed that avoids the need to wait for I/O. The method used is the *interrupt system*. When the device is ready to perform a transfer, it notifies the CPU and the transfer begins immediately. The background process being performed by the CPU is suspended to be resumed after the I/O device has been serviced. The process is as follows:  
1) A device that is ready to handle an I/O transfer sends an interrupt request to the CPU  
2) The current instruction is completed and if the request is accepted by the CPU (if its priority is high enough), the device sending the request is identified  
3) The stack frame is saved to the stack  
4) The contents of the PC are replaced with the first instruction of the device servicing routine  
5) The last instruction of this routine restores the stack frame to the CPU  
6) The background process resumes as if there had been no interruption  

Not every device has the same importance to the running of the computer. Each device is assigned a priority and interrupt requests from those devices with higher priority take precedence over requests from lower priority devices. If a high-priority request comes in during a low-priority servicing routine, the servicing routine is pushed to the stack to be resumed after the higher priority one completes. If a low-priority request comes in during a high-priority routine, it will either be pushed to the stack to be started after the current routine ends, or discarded completely.

Advantages of interrupts are that they do not waste CPU cycles testing device flags, they are typically more responsive than polling, and they can easily control multiple devices by assigning priorities. The disadvantages are that specialised hardware is needed to control the interrupts, and the context switch (pushing and popping stack frames) costs CPU time.

Another optimisation made by architectures is *Direct Memory Access (DMA)*. Without DMA, all the data transferred from an I/O device to memory must pass through a data register of the CPU. This wastes CPU time. DMA allows the I/O device (or memory) to send a request through the CPU to start a transfer. Once the transfer has been started by the CPU, the rest of the data passes directly from the I/O device's buffer to memory, bypassing the CPU. The CPU is then notified when the transfer is completed. This allows the CPU to perform useful work while the transfer completes independently, and also means the CPU can't be a rate-limiting factor between memory and a fast I/O device.
