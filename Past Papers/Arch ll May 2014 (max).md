#1

1a - Memory protection is needed to stop one program from reading or writing to the data needed by another program or the monitor/OS. It must also allow the OS to read and write to any part of memory.

1b - The memory management unit (MMU) is a special piece of hardware which contains a table of flags for the currently running (user mode) process, which say whether or not the current process can read or write to given areas of memory. Memory is split into blocks called pages (normally 4096 bytes), which is marked readable/writable as a whole. Setting the flags in the MMU is a privileged operation, so only privileged programs can change them. Every time an unprivileged process tries to perform a memory access, the MMU checks the flags to see if it is allowed to do so.

1c - When an unprivileged process tries to perform a memory access, the MMU checks it's flags to see if it is allowed to do so. If not, it raises an interrupt, passing control back to the OS which can then decide what to do with the process.

1d - Page tables contain mappings between a process's virtual addresses and the actual physical addresses. Each page in a proccess's virtual address space corresponds to a page in the physical memory. They are stored in memory as part of the process control block.

1e - The translation lookaside buffer (TLB) is a piece of hardware and part of the MMU. It keeps a copy of a small subset of the mappings from the page table of the currently running process and can translate them very quickly. This means there doesn't have to be another read to memory to find the mapping every time an instruction or data read/write is executed.

1d - Because it has to be very fast, and is therefore very expensive.

#2

2d - The programmer doesn't want to have to know the intricacies of the hardware in order to write a program, nor do they want to re-implement basic functions like print in every program, so the OS should do this for them. This saves time for the programmer, and the expert who did this presumably has more programming experience, understands the hardware well, and is familiar with OS programming, so is much more suited to the task.

2e - It should be efficient and lightweight, as each CPU cycle used by the OS is one taken from the users programs. It should also be flexible and not get in the way of the programmer, ideally completely invisible, so the programmer doesn't feel restricted by the OS.

2f - An operating system manages the resources of a computer, and provides a general programming interface to interact with the hardware. System libraries provide specific functions for interacting with hardware, handling things like maths, graphics and sound. However when OSs are marketed, these are often all bundled together (along with the GUI) as one 'OS', which leads to confusion among consumers about the layer abstraction, and which layers are part of the OS.

4a - A layering model is a suggestion on how to split the design of a standard, i.e. the different layers. Designing a standard is too big a problem to tackle all at once, so layering models are used to break the problem down into well-defined layers.

A standard is a set of rules that any implementation following the standard must follow, and specifices protocols which comply with said rules. Standards ensure interoperability between different hardware and software, i.e. machine A and machine B can communicate despite being completely different technologies and never having communicated before.

A protocol is a suggested implementation, specified by a standard. Protocols are useful because they clearly follow a specific standard, so by using a protocol can be sure you are complying with the standards, and will be able to communicate with other users of the protocol.

#5

5a - The Domain Name System (DNS) is a protocol that takes a machines name (e.g. lcpu.bath.ac.uk) and finds it's IP address, which is needed if two machines want to communicate.

5b - Each machine used to have it's own lookup table of names and addresses, however as the Internet grew this stopped being feasible.

5c - Every time a new IP address is made, or the IP address for a particular name changes, the lookup table on every single machine across the world would need to be updated, which would take an extremely long time.

If all machines names and IP addresses were stored in a single table, sorting the information whenever an item is added or updated and searching it to find a specific name or address would take an extremely long time.

5d - Assuming that the name server for the initial host is not on the same network as lcpu.bath.ac.uk and doesn't have the address cached, the following would happen:

- Host sends a DNS request for lcpu.bath.ac.uk to it's local name server (which it already knows the IP address of), say dns1.hants.uk, which sees that lcpu isn't in it's local network.
- dns1 sends a SOA request to a random top-level server, say a.root-server.net (dns1 will already know it's IP address), for the 'uk' label. a.root-server.net replies with the name and IP address of the DNS server which manages the uk label's name, say dns2.nic.uk.
- dns1 sends a SOA request to dns2.nic.uk for the 'ac.uk' label, dns2 replies with the name and IP address of the DNS server which manages 'ac.uk', say dns3.nic.uk.
- dns1 sends a SOA request to dns3.nic.uk for the 'bath.ac.uk' label, dns3 replies with the name and IP address of the DNS server which manages 'bath.ac.uk', say dns4.bath.ac.uk.
- dns1, knowing that dns4.bath.ac.uk must know the address for lcpu.bath.ac.uk, sends an address request to dns4 for lcpu.bath.ac.uk. dns4 replies with the IP address for lcpu.
- dns1 sends the IP address of lcpu.bath.ac.uk back to the initial host.
