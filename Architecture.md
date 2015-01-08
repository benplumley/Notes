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
