1a) A memory cell is the smallest addressable group of bits in main memory. The contents of a cell are fetched by putting the cell's address into the Memory Address Register. This address is then sent over the address bus and a read command is sent over the control bus. Main memory responds by placing the contents of the cell onto the data bus, which places the data into the Memory Buffer Register. The data is now in the CPU.
b) Immediate: the value immediately after the instruction is the value to use as the operand.
Direct: the value immediately after the instruction contains an address, and the cell at that address contains the value to use as the operand.
Indirect: the value after the instruction contains an address, and the cell at that address contains another address, and the cell at that second address contains the operand.
Relative: the value after the instruction contains an offset from the current instruction; the cell at the current location plus the offset contains the operand.
1c) board. To set the ouput (marked Q) to 1, raise the input marked S. To set the output to zero, raise the input marked R. Once the input has been raised, it can be dropped again immediately and the output will be retained. Raising both inputs results in undefined behaviour so is not allowed.
1d) Shared memory is one pool accessible by every processor. An advantage is that each processor can access each memory location in the same amount of time, but a disadvantage is that the von Neumann bottleneck is amplified because the memory is only capable of serving one processor at a time.
An alternative is to have separate pools of memory, one for each processor. A processor can access its own pool quickly, but it takes a long time to access memory in another processor's pool because a request has to be sent. The disadvantage of this is that two processors could perform different operations on the same data and then save the results to the same location, without knowing that the other processor had also done the same. When the memory is recombined, one of the results will be lost. This is known as the cache coherence problem.
A solution to these problems is to create a shared memory pool whose sections have different access times to different processors. A processor is encouraged to only access memory that is fastest for it, and the other processors are discouraged from using this section. However, processors can still access other processors' memory faster than they would be able to by message passing.
Another solution to the problems is to give each processor a section of memory only it can use, but also give the processors a shared pool. Cache coherence is solved because all processors can write to the same pool; the bottleneck is reduced because each processor can write to its own memory.
16/20

2) paper

3) Pipelining is a form of instruction level parallelism. It involves using redundant parts of the computer architecture to perform more than one instruction simultaneously. This works because there are five steps to performing an instruction:
1) load the operation
2) decode
3) load the operands
4) execute the instruction
5) store the result
When the first instruction is being decoded, the second can be loaded, and so on until we have five instructions ongoing, one at each stage of the cycle. This means that although the latency of a single instruction has not changed, the throughput of the processor has increased up to fivefold.

Another form of instruction level parallelism, superscalar, can be used alongside pipelining. The main difference is that where the start of two instructions is staggered in a pipeline, equal stages of multiple instructions happen simultaneously in a superscalar architecture. This uses redundant components in the processor, unlike pipelining, which uses redundant components in the whole architecture.

If an instruction set is to be designed particularly so that it will pipeline effectively, it is important that each stage of an instruction takes roughly equal time to complete, and also that each instruction as a whole takes roughly equal time from the first to last stage. This is because unequal stage times can cause the pipeline to stall, meaning one slow instruction will also slow down the other instructions sharing the pipeline with it.

As mentioned above, potential difficulties of pipelining include that not all instructions take equal time, and that not all stages take equal time. These can cause stalling of the pipeline. This problem can be reduced by carefully designing instruction sets so that all instructions and stages are roughly equal in time taken to complete. Another problem is when code execution is not linear, for instance because of a jump command. This means that the next three instructions will have begun to be processed by the time the jump is executed, meaning those three are now useless and must be discarded and the pipeline started from scratch. This can be solved by either using heuristics to work out which code path to decode or keeping multiple pipelines, one for each possible branch, and discarding all but the correct one. Another problem is dependency, where the input to one instruction depends on the output of the previous one. The problem with this is that the operands of the second are loaded before the results to the first are stored. This means that if the results of the first should have been the operands to the second, the operands that were actually loaded are no longer correct. To solve this, the processor could detect dependency and do unrelated work between two dependent instructions.

4a) Sign and magnitude, 1's complement, 2's complement. 2's complement is the most suitable for arithmetic because it is the only form where the operation to be performed does not depend on the sign of the number. With sign and magnitude form, the processor must detect the sign of both numbers in an operation, and pick the way of completing that operation specific to the pair of signs present. In 1's complement, arithmetic is easier but still requires conversions. Only in 2's complement is arithmetic identical for every possible pair of signs.
b) SM: 11110001, -43
1C: 10001110, -84
2C: 10001111, -85
c) Normalised floating point representation is a compact way of writing numbers with widely varying magnitude. The mantissa is a signed number 1<=|mantissa|<R, with the exception of zero (where the mantissa is zero). The exponent is a signed integer. The value of the number is calculated in the following way: value = mantissa * R^exponent. R, the radix, is the base of the number system being worked in: 10 in decimal, 2 in binary etc.
d) Highest power of 2 needed: 2^28
28 can be represented in 5 bits, leaving 11 bits for the mantissa
First 11 bits of 299792458 in unsigned binary: 100011101111
28 in unsigned binary: 11100
So mantissa = 100011101111, exponent = 11100
Combined, the two byte representation is 10001110111111100. The first 11 bits are the unsigned mantissa, and the last five bits are the unsigned exponent. The implied binary point is after the first bit. My approximation's accuracy is 11 binary places, and converted back into decimal, it is accurate to 4 decimal places. In decimal, my approximation is 30,794 smaller than the actual value.

5d)
Operands preceded by a # are immediate. Operands with no preceding sign are direct. Operands preceded by a $ are indexed relative to location 2000 (so an operand $1 refers to the value at address 2001).

1	LOAD3 #0
2	ADD1 $R2
3	DEC2 #5
4	DEC3 #2
5
