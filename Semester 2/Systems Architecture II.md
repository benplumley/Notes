#CM10195 - Systems Architecture
##Dr Russel Bradford

An operating system is a program (often called the kernel) which:
- Manages the resources of the computer e.g. CPU, memory, keyboard, and any software that controls it.
- Provides the programmer with a usable programming interface to access those resources
The interface that the end user interacts with is just another program that uses the OS, *not* a part of the OS.

####Managing Resources

There are 3 main reasons for managing resources:
- They are limited - There is not always enough resources to go round, e.g. mobile phones have strict limtations on memory,
CPU power and energy consumption.
- They need protection - This includes security (preventing programs from corrupting data or other programs), authorisation (ensuring that certain resources are only available to certain programs), authentication (ensuring that a program has the authorisation it claims to have), and protecting the user from their own mistakes (e.g. accidentally deleting files).
- They need to meet certain criteria - This includes responsiveness (the program needs to respond quickly, or process network packets as they arrive), real time (certain events *must* be dealt with in a fixed amount of time e.g. video streaming), security (prevention of accidental or malicious access or modification.

####Programming Interface

The programmer who was to write applications for the machine does not want to have to know the details of the hardware, and they dont want to have to re-implement everything in every program, so the OS does this for them. Having an expert do this and provide a standard interface is a lot more practical. It means:
- The programmer doesn't have to do it, therefore saving time.
- The expert presumably has more programming experience, understands the hardware well, and is familiar with the intricacies of OS programming.

The different layers are often confused with eachother. People often confuse the GUI and some applications as part of the OS - this is largely due to marketers advertising their operating systems based on the GUI. However this is a misconception, for example embedded systems massively outsell PCs and most of these do not have even the most basic of user interfaces.

Here are two examples of layer abstraction, one good and one bad.

Good:
![alt-text](http://i.gyazo.com/ee70ee4899e5a1dcf225f8c5e37fbb72.png)

Bad:  
![alt-text](http://i.gyazo.com/598248022cb159db1a309ec5f1f9e0f6.png)

An OS should be efficient and lightweight: every CPU cycle that the OS uses is one that is taken awaay from the user's programs. It should also be flexible and not get in the way of the programmer - so a perfect OS would be completely invisible.

####Background

An OS is just a program, so we can have differents OSs on the same hardware, and the same OS on different hardware, e.g. on intel hardware (PC) you can run Windows, OS X, Linux and many others. Since an OS has to deal with the details of hardware, it is not entirely trivial to port on OS from one architecture to another. Well designed OSs mninimise the hardware dependent parts and try to keep mose code hardware-independent. Historically, some OSs tied themselves too closely to the hardware so that porting was very difficult. For example, for much of its lifetime Windows only ran on Intel, so the assumption of Intel hardware ran throughout the code. In contrast, the Android OS shares a large amount of code with the Linux that runs everywhere else.

The general public often think of the OS as the GUI (there is some basis for this confusion, as Microsoft and Apple tie their GUIs indivisibly to their OSs), and some software companies encourage and make capital out of this confusion.

####History

At first, computers had no operationg systems (1960s) - every programmer had to write their programs for the particular machine they were using, and therefore had to know exactly what kind of hardware they had and how to use it. This meant there was no portability, and lots of repeated code between programs.

In fact, programmers rarely even saw the computer. The program and the data (collectively called a job) would be prepared on paper tape or punched card. Jobs would be given to operators who would load and run them, then give the results back. Usually there would be a bug and the programmer would have to fix the program and go round the loop again. Computer time was limited, so scheduling the jobs for the computer was done by hand. Turnaround on these jobs could be days.

Due to the amount of repeated code between programs, common functions were collected in system libraries (sqrt, openfile etc). Other useful tools developed were debuggers, interfacing to hardware (I/O drivers), and program managements (loaders). These made programming much easier, but there was still lots of human intervention needed.

The issue was to minimise idle time for the big and expensive computer, as this was a waste of money. So the operators would load many programs on to a fast medium, such as magnetic tape, and the computer would load programs from that, sometimes loading several programs at once and then running each of them in turn. This was called *spooling*.Spooling was also used on output - the outputs would be written to a magnetic tape, which could then later be attached to a printer (becuase printers are slower than computers).

It soon became clear that this could be automated, so a program called a monitor (or supervisor) that loads and runs programs and puts the results somewhere sensible was created. This would be directed by a *job control language* (e.g. JCL). JCL allowed:
- Different classes of job - some people were allowed more time or memory space than others.
- Automatic accounting - automatically charge for CPU time, memory usage etc.
- Programmers could specify things like when they want the program to run, how much disk or memory it needs etc. If a job ran out of its alloted time or space it would be killed.
JCL also allowed *batch processing* - several programs are collected and loaded together in a single bunch. Running in batches is more efficient, as we spend more time running our programs and less time messing around in the overheads of loading and unloading. Batch processing and charging still happen today - modern large computers (like Bath's Aquila) are managed in just this way, and the popular 'cloud computing' is just a modern marketing term for batch processing.

####The Monitor and Interrupts

The monitor is just a program. It loads the programmers application into memory (from tape or wherever), and then jumps to the start of the application to start executing it. Once it has finished, it would jump back to the monitor to deal with the next program. However, if the program was badly written, it could overrite the monitor (either accidentally or deliberately).
It was soon found more efficient to load more than one program into memory, the advantage being that if program 1 was doing something like writing to tape that takes lots of time, but no CPU, the computer could run program 2 in the meantime - this is called multitasking. When program 2 pauses and program 1 needs to run again, the computer just switches back. These decisions about what to run and the switches between programs are handled by the monitor, and are influenced by factors such as how long a program has been running, the priority of a program, whether it is likely to need the CPU very soon or it can wait, how much the owner has paid etc. There is a trade of between making the scheduling fast but fair. If it is too basic some programs could take advantage of this and starve other programs of CPU time. If it is too complicated it means more time deciding what to run and less time actually running programs. This is still an issue today.

The issue with multitasking is that program 1 can now corrupt program 2 *and* the monitor, as well as read confidential data out of program 2. Also if program 1 goes into an infinite loop, control never returns to the monitor and program 2 never runs. This can be solved with *interrupts*. A hardware clock or timer can be set to send interrupts regularly after an appropriate period of time has elapsed. When the interrupt is taken, the interrupt sevice routine jumps to the monitor so it can decide what to do next, including:
- Resume running the interrupted program
- Kill the program if it has used up its allotted resources
- Switch to running some other program

Similarly, interrupts from peripherals like terminals or disks pass control to the monitor. This is called *preemptive scheduling*, and enables *timesharing* - where several programs share the available CPU time and so appear to be running simultaneously.

This interrupt mechanism allowed the use of *terminals*, allowing users to interact directly with the computer rather than just via job submission. A program can sit and wait (i.e. not be scheduled to run by the monitor) until the user hits a key on the terminal. When a key is hit, an interrupt happens, the monitor takes over, and chooses to run (schedules) the appropriate program to deal with the keystroke. Thus the program uses no CPU resources until they are needed. This is another way of bridging the gap between slow humans and fast computers.

Timer intterupts are typically set to go off fairly often, meaning several programs can get a slice of the CPU quite often. With sufficiently frequent interrupts it appears to a human observer that serveral programs are running simultaneously. An *interactive* program will appear to be dedicated to that user - in reality humans are so slow we can't appreciate how little time the computer gives us. It is important to remember that a single processor can only do one thing at a time - it is only the appearance of multiple programs running simultaneously.

On the other hand, too frequent interrupts mean the monitor is forever being called and using CPU time, so less time is available for the progrums. This is another tradeoff - frequent interrupts for good interactive behaviour, or fewer interrupts for good compute behaviour. Therefore we need clever scheduling algorithms in the monitor to try to give high priority but small slices of time to interactive programs, and lower priority but larger slices to compute-intensive programs.

A 'large slice of time' means the monitor will allow a program to continue running for a relatively long amount of time before scheduling a different program, i.e. the monitor will continue to schedule the program through several interrupts. A 'small slice of time' means the monitor will deschedule the program after only a brief amount of running time, perhaps just a few interrupts. Thus, the monitor can deal out CPU time to the programs in appropriately sized chunks - this is all part of the scheduling decision computations that happen potentially every time the monitor runs.

Low power gadgets like to keep the number of interrupts down, as this increases the amount of time the CPU can be idling in low power *sleep states* - an interrupt is a wake up call that the CPU must deal with. Tuning an OS is very difficult and depends critically on the applications it needs to run. When an OS spends more time deciding what to do than doing useful work, it is called *thrashing*, a problem many early OSs had.

Certain operations like accessing tape or a printer must be reserved for use by the monitor, and not be accesible by a random user program. In the CPU, machine instructions are divivded into two (or more) classes, unprivileged operations (arithmetic, tests, jumps) which any program can execute, and privileged operations (like access to peripherals) that only certain programs can run. The processor can also run in two (or more) modes; unprivileged, called the user mode and used for normal computation, and privileged, called the kernel mode and used for systems operation. Some processor architectures have four or more levels of privilege, sometimes using a ring system. Note that privelege is a state of the processor.

Privilege is a state of the processor, not the program, but we tend to say "a privileged program" rather than "a program running with the CPU in privileged mode". If an unprivileged program tries to execute a privileged operation, the hardware causes an interrupt (also called a system trap) and sets the processor to privileged mode. The interrupt service routine then jumps back to the monitor program, which decides what to do next e.g. disallow the operation, kill the program.

The system starts in kernel (privileged) mode:
1. The monitor decides which process to schedule
2. It restores the state of the program, then uses a special jump-and-drop-privilege instruction to start running the program
3. The program runs unprivileged (user mode)
4. The program finishes or decides it needs a system resource, so it should call the monitor
5. The program executes a special “call monitor” (or syscall) instruction that jumps to the monitor
6. This special jump also enables privileged mode, so the monitor regains control with privilege
7. The monitor saves the state of the program, then decides what to do next

The syscall instruction always jumps to the monitor, so the program cannot use it to gain privilege for itself. The jumping between modes ensures that the monitor is runing in privileged mode and the user program is running in unprivileged mode. The user program can never get into privileged mode, as every transition to privileged mode is tied by the hardware to a jump to the monitor. Forcing access to hardware via the monitor also provides protection and management for other system resources, like access to files or the network. System libraries often include some nicer interfaces to the syscalls, wrapping them to make them easier to use e.g. the 'open file' syscall might need a file name to be place in certain registers.

Switching in and out of kernel mode is a relatively time consuming operation in many OSs, due to overheads like saving and restoring the CPU state of the running process.

The next issue is memory protection - stopping a program from reading and writing the memory used by another program or the monitor/OS. The OS must be allowed to read and write any part of memory. There is a table of flags in a special piece of hardware, the *memory management unit* (MMU). These flag say whether the currently running (user mode) program can read or write a given area of memory. A diagram showing this can be seen below:

![](http://i.gyazo.com/047e176cb2ddf8eaacc99e38304a2c64.png)

Setting the flags in the MMU is a privileged operation. On every memory access by an unprivileged program, the MMU checks the flags to see if that access is allowed, and if not, raises an interrupt and the OS takes control again. Doing this on a byte-by-byte level wouldn't be feasible, so memory is divided into blocks called pages. A page is just a continuous area of memory (4096 bytes is popular on modern machines, though current hardware can support 4mb pages). The page is marked as read/writable as a whole, which makes technique more practicle. Each process has its own set of flags, and this is part of the process's state that must be saved and restored when that process is resheduled. There is often also a third, executable flag - can you execute code at this memory address?

####Proccesses

The word **process** is used to describe the executable code, its data and the associated information the OS needs to run it. A single program might use more than one process, for example one press to compute a picture and another to display it. This is called *structure by process*. However this is somewhat of an exception these days, quite often a program uses just one process, and structuring can be done by using multiple threads of execution.

An OS needs to keep lots of information about a process, which it uses to schedule and protect the process. This information includes:
- Where in memory it is (the code)
- What parts of memory belong to it (the data)
- What permissions it has on those parts of memory (flags from the MMU)
- How much time it is allocated
- How much time it has used
- Similarly for other shared resources, e.g. the amount of I/O done
- The CPU's PC and registers
- And more...

A process can be in one of several states. There are 5 main states (although real OSs have many more than this):
1. New - A process that has just been created
2. Running - It is currently executing on the CPU
3. Ready - It is ready to run, but some other process (or the OS) is currently using the CPU
4. Blocked - Waiting for some event or resource to become available e.g. waiting for some data to arrive from the disk
5. Exit - A process that has finished

The OS will be managing many processes, and keeps lists of which processes are in which state, so scheduling is simply making the choice of which process to move between which states. In real OSs, for efficiency, these will not be simple lists - they may be arranged in priority order, or maybe some more sophisticated datastructure e.g. a tree (like in Unix). This allows control of a group of processes. A group within the tree has a *session leader*, which would typically kill all the processes in the group if it is killed.

There is a standard finite state machine which describes the allowed transitions between states:

![](http://i.gyazo.com/5c0a2ed582b54ce84269ebf030098f6a.png)

A typical transition is:
1. The OS decides to schedule a process on the ready list
2. The process is dispatched - the OS marks its state as running and starts executing it (jump and drop privilege)
3. The process may choose to voluntarily suspend itself - *relinquish* (e.g. a clock program displaying the time might suspend itself for a minute).
4. An interrupt may arise, e.g. from a packet arriving on the network card, or a key being hit on the keyboard.
5. Alternatively, a timer interrupt may happenw hen the process has used its time slice.
6. Or the process may *block* - when it needs some resource the OS must supply (so it does a syscall) and must wait until the resource is ready (e.g. when the disk returns some data)
7.