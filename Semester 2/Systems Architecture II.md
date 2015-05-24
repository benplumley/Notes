#CM10195 - Systems Architecture
##Dr Russel Bradford

An operating system is a program (often called the kernel) which:
- Manages the resources of the computer e.g. CPU, memory, keyboard, and any software that controls it.
- Provides the programmer with a usable programming interface to access those resources
The interface that the end user interacts with is just another program that uses the OS, *not* a part of the OS.

####Managing Resources

There are 3 main reasons for managing resources:
- They are limited - There is not always enough resources to go round, e.g. mobile phones have strict limitations on memory,
CPU power and energy consumption.
- They need protection - This includes security (preventing programs from corrupting data or other programs), authorisation (ensuring that certain resources are only available to certain programs), authentication (ensuring that a program has the authorisation it claims to have), and protecting the user from their own mistakes (e.g. accidentally deleting files).
- They need to meet certain criteria - This includes responsiveness (the program needs to respond quickly, or process network packets as they arrive), real time (certain events *must* be dealt with in a fixed amount of time e.g. video streaming), security (prevention of accidental or malicious access or modification).

####Programming Interface

The programmer who has to write applications for the machine does not want to have to know the details of the hardware, and they don't want to have to re-implement everything in every program, so the OS does this for them. Having an expert do this and provide a standard interface is a lot more practical. It means:
- The programmer doesn't have to do it, therefore saving time.
- The expert presumably has more programming experience, understands the hardware well, and is familiar with the intricacies of OS programming.

The different layers are often confused with each other. People often confuse the GUI and some applications as part of the OS - this is largely due to marketers advertising their operating systems based on the GUI. However this is a misconception, for example embedded systems massively outsell PCs and most of these do not have even the most basic of user interfaces.

Here are two examples of layer abstraction, one good and one bad.

Good:  
![alt-text](http://i.gyazo.com/ee70ee4899e5a1dcf225f8c5e37fbb72.png)

Bad:  
![alt-text](http://i.gyazo.com/598248022cb159db1a309ec5f1f9e0f6.png)

An OS should be efficient and lightweight: every CPU cycle that the OS uses is one that is taken away from the user's programs. It should also be flexible and not get in the way of the programmer - so a perfect OS would be completely invisible.

####Background

An OS is just a program, so we can have differents OSs on the same hardware, and the same OS on different hardware, e.g. on intel hardware (PC) you can run Windows, OS X, Linux and many others. Since an OS has to deal with the details of hardware, it is not entirely trivial to port on OS from one architecture to another. Well designed OSs minimise the hardware dependent parts and try to keep most code hardware-independent. Historically, some OSs tied themselves too closely to the hardware so that porting was very difficult. For example, for much of its lifetime Windows only ran on Intel, so the assumption of Intel hardware ran throughout the code. In contrast, the Android OS shares a large amount of code with the Linux that runs everywhere else.

The general public often think of the OS as the GUI (there is some basis for this confusion, as Microsoft and Apple tie their GUIs indivisibly to their OSs), and some software companies encourage and make capital out of this confusion.

####History

At first, computers had no operating systems (1960s) - every programmer had to write their programs for the particular machine they were using, and therefore had to know exactly what kind of hardware they had and how to use it. This meant there was no portability, and lots of repeated code between programs.

In fact, programmers rarely even saw the computer. The program and the data (collectively called a job) would be prepared on paper tape or punched card. Jobs would be given to operators who would load and run them, then give the results back. Usually there would be a bug and the programmer would have to fix the program and go round the loop again. Computer time was limited, so scheduling the jobs for the computer was done by hand. Turnaround on these jobs could be days.

Due to the amount of repeated code between programs, common functions were collected in system libraries (sqrt, openfile etc). Other useful tools developed were debuggers, interfacing to hardware (I/O drivers), and program managements (loaders). These made programming much easier, but there was still lots of human intervention needed.

The issue was to minimise idle time for the big and expensive computer, as this was a waste of money. So the operators would load many programs on to a fast medium, such as magnetic tape, and the computer would load programs from that, sometimes loading several programs at once and then running each of them in turn. This was called **spooling**. Spooling was also used on output - the outputs would be written to a magnetic tape, which could then later be attached to a printer (becuase printers are slower than computers).

It soon became clear that this could be automated, so a program called a monitor (or supervisor) that loads and runs programs and puts the results somewhere sensible was created. This would be directed by a **job control language** (e.g. JCL). JCL allowed:
- Different classes of job - some people were allowed more time or memory space than others.
- Automatic accounting - automatically charge for CPU time, memory usage etc.
- Programmers could specify things like when they want the program to run, how much disk or memory it needs etc. If a job ran out of its alloted time or space it would be killed.
JCL also allowed **batch processing** - several programs are collected and loaded together in a single bunch. Running in batches is more efficient, as we spend more time running our programs and less time messing around in the overheads of loading and unloading. Batch processing and charging still happen today - modern large computers (like Bath's Aquila) are managed in just this way, and the popular 'cloud computing' is just a modern marketing term for batch processing.

####The Monitor and Interrupts

The monitor is just a program. It loads the programmers application into memory (from tape or wherever), and then jumps to the start of the application to start executing it. Once it has finished, it would jump back to the monitor to deal with the next program. However, if the program was badly written, it could overwrite the monitor (either accidentally or deliberately).
It was soon found more efficient to load more than one program into memory, the advantage being that if program 1 was doing something like writing to tape that takes lots of time, but no CPU, the computer could run program 2 in the meantime - this is called multitasking. When program 2 pauses and program 1 needs to run again, the computer just switches back. These decisions about what to run and the switches between programs are handled by the monitor, and are influenced by factors such as how long a program has been running, the priority of a program, whether it is likely to need the CPU very soon or it can wait, how much the owner has paid etc. There is a trade of between making the scheduling fast but fair. If it is too basic some programs could take advantage of this and starve other programs of CPU time. If it is too complicated it means more time deciding what to run and less time actually running programs. This is still an issue today.

The issue with multitasking is that program 1 can now corrupt program 2 *and* the monitor, as well as read confidential data out of program 2. Also if program 1 goes into an infinite loop, control never returns to the monitor and program 2 never runs. This can be solved with **interrupts**. A hardware clock or timer can be set to send interrupts regularly after an appropriate period of time has elapsed. When the interrupt is taken, the interrupt sevice routine jumps to the monitor so it can decide what to do next, including:
- Resume running the interrupted program
- Kill the program if it has used up its allotted resources
- Switch to running some other program

Similarly, interrupts from peripherals like terminals or disks pass control to the monitor. This is called **preemptive scheduling**, and enables **timesharing** - where several programs share the available CPU time and so appear to be running simultaneously.

This interrupt mechanism allowed the use of **terminals**, allowing users to interact directly with the computer rather than just via job submission. A program can sit and wait (i.e. not be scheduled to run by the monitor) until the user hits a key on the terminal. When a key is hit, an interrupt happens, the monitor takes over, and chooses to run (schedules) the appropriate program to deal with the keystroke. Thus the program uses no CPU resources until they are needed. This is another way of bridging the gap between slow humans and fast computers.

Timer intterupts are typically set to go off fairly often, meaning several programs can get a slice of the CPU quite often. With sufficiently frequent interrupts it appears to a human observer that several programs are running simultaneously. An *interactive* program will appear to be dedicated to that user - in reality humans are so slow we can't appreciate how little time the computer gives us. It is important to remember that a single processor can only do one thing at a time - it is only the appearance of multiple programs running simultaneously.

On the other hand, too frequent interrupts mean the monitor is forever being called and using CPU time, so less time is available for the programs. This is another tradeoff - frequent interrupts for good interactive behaviour, or fewer interrupts for good compute behaviour. Therefore we need clever scheduling algorithms in the monitor to try to give high priority but small slices of time to interactive programs, and lower priority but larger slices to compute-intensive programs.

A 'large slice of time' means the monitor will allow a program to continue running for a relatively long amount of time before scheduling a different program, i.e. the monitor will continue to schedule the program through several interrupts. A 'small slice of time' means the monitor will deschedule the program after only a brief amount of running time, perhaps just a few interrupts. Thus, the monitor can deal out CPU time to the programs in appropriately sized chunks - this is all part of the scheduling decision computations that happen potentially every time the monitor runs.

Low power gadgets like to keep the number of interrupts down, as this increases the amount of time the CPU can be idling in low power *sleep states* - an interrupt is a wake up call that the CPU must deal with. Tuning an OS is very difficult and depends critically on the applications it needs to run. When an OS spends more time deciding what to do than doing useful work, it is called **thrashing**, a problem many early OSs had.

Certain operations like accessing tape or a printer must be reserved for use by the monitor, and not be accesible by a random user program. In the CPU, machine instructions are divided into two (or more) classes, unprivileged operations (arithmetic, tests, jumps) which any program can execute, and privileged operations (like access to peripherals) that only certain programs can run. The processor can also run in two (or more) modes; unprivileged, called the user mode and used for normal computation, and privileged, called the kernel mode and used for systems operation. Some processor architectures have four or more levels of privilege, sometimes using a ring system. Note that privilege is a state of the processor.

Privilege is a state of the processor, not the program, but we tend to say "a privileged program" rather than "a program running with the CPU in privileged mode". If an unprivileged program tries to execute a privileged operation, the hardware causes an interrupt (also called a system trap) and sets the processor to privileged mode. The interrupt service routine then jumps back to the monitor program, which decides what to do next e.g. disallow the operation, kill the program.

The system starts in kernel (privileged) mode:  
1. The monitor decides which process to schedule  
2. It restores the state of the program, then uses a special jump-and-drop-privilege instruction to start running the program  
3. The program runs unprivileged (user mode)  
4. The program finishes or decides it needs a system resource, so it should call the monitor  
5. The program executes a special “call monitor” (or syscall) instruction that jumps to the monitor  
6. This special jump also enables privileged mode, so the monitor regains control with privilege  
7. The monitor saves the state of the program, then decides what to do next  

The syscall instruction always jumps to the monitor, so the program cannot use it to gain privilege for itself. The jumping between modes ensures that the monitor is runing in privileged mode and the user program is running in unprivileged mode. The user program can never get into privileged mode, as every transition to privileged mode is tied by the hardware to a jump to the monitor. Forcing access to hardware via the monitor also provides protection and management for other system resources, like access to files or the network. System libraries often include some nicer interfaces to the syscalls, wrapping them to make them easier to use e.g. the 'open file' syscall might need a file name to be placed in certain registers.

Switching in and out of kernel mode is a relatively time consuming operation in many OSs, due to overheads like saving and restoring the CPU state of the running process.

The next issue is memory protection - stopping a program from reading and writing the memory used by another program or the monitor/OS. The OS must be allowed to read and write any part of memory. There is a table of flags in a special piece of hardware, the **memory management unit** (MMU). These flag say whether the currently running (user mode) program can read or write a given area of memory. A diagram showing this can be seen below:

![](http://i.gyazo.com/047e176cb2ddf8eaacc99e38304a2c64.png)

Setting the flags in the MMU is a privileged operation. On every memory access by an unprivileged program, the MMU checks the flags to see if that access is allowed, and if not, raises an interrupt and the OS takes control again. Doing this on a byte-by-byte level wouldn't be feasible, so memory is divided into blocks called pages. A page is just a continuous area of memory (4096 bytes is popular on modern machines, though current hardware can support 4mb pages). The page is marked as read/writable as a whole, which makes technique more practical. Each process has its own set of flags, and this is part of the process's state that must be saved and restored when that process is resheduled. There is often also a third, executable flag - can you execute code at this memory address?

####Processes

The word **process** is used to describe the executable code, its data and the associated information the OS needs to run it. A single program might use more than one process, for example one process to compute a picture and another to display it. This is called **structure by process**. However this is somewhat of an exception these days, quite often a program uses just one process, and structuring can be done by using multiple threads of execution.

An OS needs to keep lots of information about a process, which it uses to schedule and protect the process. This information includes:
- Where in memory it is (the code)
- What parts of memory belong to it (the data)
- What permissions it has on those parts of memory (flags from the MMU)
- How much time it is allocated
- How much time it has used
- Similarly for other shared resources, e.g. the amount of I/O done
- The CPU's PC and registers
- And more...

A process can be in one of several states. There are 5 main states which the OS moves processes between (although real OSs have many more than this):  
1. New - A process that has just been created, perhaps code and data are not yet loaded into memory. The OS data structures needed to manage the process have been created and filled in.  
2. Running - It is currently executing on the CPU.  
3. Ready - It is ready to run, but some other process (or the OS) is currently using the CPU.  
4. Blocked - Waiting for some event or resource to become available e.g. waiting for some data to arrive from the disk.  
5. Exit - A process that has just finished. Some tidying up is usually needed after a process ends, such as closing files or reclaiming memory or other resources used for its running or management.

The OS will be managing many processes, and keeps lists of which processes are in which state, so scheduling is simply making the choice of which process to move between which states. In real OSs, for efficiency, these will not be simple lists - they may be arranged in priority order, or maybe some more sophisticated datastructure e.g. a tree (like in Unix). This allows control of a group of processes. A group within the tree has a *session leader*, which would typically kill all the processes in the group if it is killed.

There is a standard finite state machine which describes the allowed transitions between states:

![](http://i.gyazo.com/5c0a2ed582b54ce84269ebf030098f6a.png)

A typical transition is:  
1. The OS decides to schedule a process on the ready list  
2. The process is dispatched - the OS marks its state as running and starts executing it (jump and drop privilege)  
3. The process may choose to voluntarily suspend itself - *relinquish* (e.g. a clock program displaying the time might suspend itself for a minute).  
4. An interrupt may arise, e.g. from a packet arriving on the network card, or a key being hit on the keyboard.  
5. Alternatively, a timer interrupt may happen when the process has used its time slice.  
6. Or the process may *block* - when it needs some resource the OS must supply (so it does a syscall) and must wait until the resource is ready (e.g. when the disk returns some data)  
7. In the case of a blocked process, data may have returned from the disk and the process can wake up and become ready again. The process won't generally start running immediately, it is just ready to run when it gets its chance. Early OSs without timer interrupts had to rely on processes relinquishing control every now and then - this is cooperative multitasking.

The **process control block**, or PCB, is the collection of data that a process needs. It contains information like user ids, a priority, statistics like memory and cpu used, the state, and lists of the resources used (in particular the memory for the code and its data). To pause and restart a running process (e.g. on an interrupt) requires saving and restoring the processor state: CPU registers, stack pointers etc. This will also be stored in the PCB. So process handling is very similar to the way interrupts are handled, but with a lot more data that needs to be saved.

Creation of a process involves the following steps:
- Allocate and create a PCB structure
- Find a free PID (process identifier - an integer that uniquely identifies this process)
- Insert the PCB into the "New" scheduling list
- Determine and allocate the necessary resources (particularly memory)
- Determine the initial priority of the process

This is what happens in the New state - it can then move to Ready when the OS decides it is time to do so. Again, the process might not start running immediately as there could be some higher priority process that must run first. Most processes are created (forked/spawned) by other processes. Of course, only the OS can actually create processes. When a process wants a new process to be created, it needs to ask the OS to do so. The OS than creates a new process according to the specifications given. The original calling process will generally be the parent of the new process. However, the OS can choose not to create the new process if some policy says not to, or there is not enough memory (or any other reason). In this case, the original process gets a message back explaining the problem.

This creates a problem however: If processes are always created by other processes, how do we get started? This is the **bootstrapping problem**. In Unix, there is an ancestor process called init with PID 1, that gets created at switch on time and it serves to create all other processes. Bootstrapping is complicated as it has to determine the hardware and how it is connected and initialise it, set up all the appropriate datastructures the OS needs, start lots of service processes running, all before it can begin to look at what the user wants. This is quite often simply called *booting*.

####Scheduling

**Scheduling** is the issue of choosing which process to run next, and is an extremely difficult problem. These are some of the problems:
- Giving each process its fair share of CPU time
- No starvation of any process
- Make interactive processes respond in human timescales
- Give as much computation time as possible to compute-heavy processes
- Ensuring critical real-time processes are dealt with before it is too late
- Service peripherals in a timely way
- Understanding the various requirements of the hardware: mice and printers are slow, while networks and disks are fast
- Distribute work amongst multiple devices e.g. CPUs and networks
- Make best use of the hardware and use it efficiently
- Make the system behaviour predictable - we don't want wildly erratic behaviour
- Try to degrade gracefully under heavy load

And all of this must be done quickly. Scheduling can be divided into three classes, each addressing different resource concerns:
- Short term - Effective use of the CPU. Which of the ready processes to run next.
- Medium term - Deciding which processes to keep or load into memory.
- Long term - Deciding which processes to admit into the scheduling system, ensuring there are enough resources to get it started.

Long term decides which processes should be considered by the medium term scheduler, medium term decides which processes should be considered by the short term scheduler, and short term decides which process should be considered to be run. Long term scheduling was an issue in the 60s and 70s when resources were more limited, but is not so relevant these days due to alternative approaches (virtual resources).

Measurements used in sheduling algorithms include CPU cycles used by the process, memory used, disk used, network used etc. We can also quantify the results:
- Throughput - more of fewer jobs finished in a given time
- Turnaround (response time) - interactive response should be snappy
- Real time - e.g. this data *must* be dealt with now else the car will crash
- Money - we've been given money to get this data ready in the next hour

This information was originally collected to calculate how much money to charge the user (cloud services still sell time on their machines like this), but nowadays we generally own our own computers, so are more concerned about making the best use of it. Here are some simple scheduling algorithms:

**Run until completion** - first in first out (FIFO), non-preemptive batch, as on pre-OS machines. Not really suitable for most modern machines (although still the basis for large clusters and the Grid).
- Good for large amounts of computation
- No overheads of multitasking
- Poor interaction with other hardware - can't process while printing (spooling)
- No interactivity

**Shortest job first** - The shortest time to completion process runs next. Non-preemptive.
- No multitasking
- Good throughput
- Similar behaviour to FIFO on average
- Long jobs suffer and might get starved
- Difficult to estimate time-to-completion

**Run until completion + cooperative multitasking** - Non preemptive. Was used on millions of computers until relatively recently.
- Weak multitasking
- Needs round-robin or something more sophisticated to choose another task on relinquish
- Poor utilisation of hardware
- Poor interactivity
- Easy for a process to starve other processes
- Hard to write "good citizen" programs

**Preemptive round robin** - Gives each process a fixed time slice.
- Multitasking
- Better utilisation of hardware
- No starvation
- Gives interactive processes the same time as compute processes
- Not good for interactive or real time - may have to wait a long time for a slice of time.

**Round robin** is more suited to systems where all the processes are of equal importance, e.g. dedicated appliances like network routers that have to decide how to share network capacity fairly. However we need to tweak round robin a bit first - it needs to take interactivity, priority etc. into account. To know if a process is interactive or compute intensive, watch how much I/O is happening and how long we are waiting for it; high I/O per compute is interactive, low is compute intensive. A process can be a mix of both, or it might move between the two over time.

Similarly, priorities can be:
- Static - Unchanging through the life of the process. Simple, but unresponsive to change (e.g. a process that alternates inactivity with urgent computation).
- Dynamic - Priority responds to changes in the load. Harder to get right, and more expensive to compute.
- Purchased - The more you pay, the higher the priority.

**Shortest remaining time** - Have a time slice, pick the next process by the estimate of the shortest time remaining. Preemptive.
- This is a round robing version of shortest job first.
- Still hard to make estimates.
- Good for short jobs.
- Long jobs can still be starved.

**Least completed next** - The process that has consumed the least amount of CPU time goes next.
- All processes make equal process in terms of CPU time.
- Interactive processes get good attention as they use relatively little CPU.
- Long jobs can be starved by lots of small jobs.

**Highest response ratio next** - A variation of shortest remaining time, where we take the time a process has been waiting since its last time slice into account. The formula is:

![](http://i.gyazo.com/9dbd1d140709dbf115975196dc6d6b11.png)

- A process executes repeated time slices until its priority drops below that of another process.
- Trieds to avoid starvation.
- Long jobs will eventually get a slice.
- New jobs will get immediate attention as CPU time is near 0
- But now critical shorter jobs might not finish in time as they could get scheduled after a long waiting job. This needs frequent re-evaluation of priorities to get good behaviour, which implies small timeslices, and so lots of scheduling overhead.

**Multilevel feedback queueing** - Can be used when we have no estimates on run times.
- There are multiple FIFO run queues, RQ0, RQ1, ..., RQn, where RQ0 is highest priority and RQn the lowest.
- Queues are processed in FIFO fashion, in priority order, so RQ1 does not get a look-in until RQ0 has emptied.
- Each process is allocated a *quantum* of time (a timeslice).
- A new process is admitted to the end of RQ0.
- When the running process has used its quantum of time, it is interrupted and placed at the end of the next lower queue (demoted).
- If the running process relinquishes voluntarily before the end of the quantum, it gets placed back at the end of the *same* queue.
- If it blocks for I/O, it will be promoted and placed at the end of the next higher queue (when ready to run).
- Demoted processes in RQn get placed at the end of RQn.
- Gives newer, shorter processes priority over older, longer ones.
- I/O processes tend to rise, getting more priority.
- Compute processes tend to sink, getting less.

With this algorithm the old processes tend to starve, so a variant of this doubles the quantum for each level - RQ0 gets 1, RQ1 gets 2, RQ2 gets 4 etc. So compute intensive processes get a big bite, whenever they get a chance, at the potential cost of responsiveness to a new process. This scheme was used by Windows NT and Unix derivatives.

Multilevel feedback queueing diagram:
![](http://i.gyazo.com/048af5ba35c7fe67c18adb847a2a8946.png)

**Traditional Unix scheduling** - As used in older Unix derivatives (modern scheduling is much more sophisticated). Everything is based on timer interrupts every 1/60th of a second. A priority is computed from the CPU use of each process:

![](http://i.gyazo.com/2b68b6ee8d253133f37a8890b186f374.png)

A process with the smallest priority value is chosen next (i.e. a process that has used less CPU). Processes of the same priority are treated round robin. This is actually very similar to multilevel feedback queueing where each priority corresponds to a queue. The base priority depends on whether this is a system process or a user process, with user priority being lower (i.e. a larger value). The CPU time recorded is halved every second. This decays the influence of CPU usage over time, and makes the priority based on recent bahaviour. This algorithm gives more attention to processes that have used less CPU recently, e.g. interactive and I/O processes.

With this, processes can choose to be *nice*. This is a value which gets added to the priority of that prosess. Generally, -20 <= nice <= 19, but only privileged users (administrators) can use negative nices. A process that has nice -20 can really jam up the system. But nice also enables a purchased priority.

There are a few problems with traditional Unix scheduling. The priorities were recomputed once per second, all in a single pass, taking a significant chunk of time (on old machines). It does not respond fast enough to dynamic changes in the system, and doesn't scale to large numbers of processes. So this isn't used in modern systems, where many 100s of processes is common. There are also other problems to address, e.g. if there are two users running simultaneously on one machine, and user A has 9 processes while user B has 1, should user A get 90% of the CPU time and B 10%?

**Fair share scheduling** - Where each user gets a fair share, rather than each process. Modern Unix derivatives use much better and more complicated scheduling algorithms than this. The priority is calculated like this:

![](http://i.gyazo.com/dd1737b9ce0d6965d9d0da73d594076e.png)

All of these algorithms only handle scheduling of one resource - the CPU. There are new issues that arise when scheduling multiple resources.

####Deadlock

Processes compete for resources like disks and networks, and the OS mediates this. To read from the disk, a process must call the OS kernel and wait for the kernel to reply. When we say a "a process waits for the kernel", what actually happens is the kernel marks the process as blocked, and does not consider it for scheduling until the requested resource has arrived. There is no "waiting" happening - the process does not run when blocked.

Say process P1 wants to copy some data from disk D1 to disk D2, while process P2 wants to copy some data from D2 to D1. The OS (rather stupidly) gives P1 exclusive access to D2 and P2 exclusive access to D1. The OS then runs P1, which requests an access to D1, but P2 has locked it so P1 must wait, and is therefore moved to the block state. The OS then runs P2 which requests an access to D2, but P1 has locked it so P2 must wait, and is moved to the block state. Now both processes are blocked and the OS can't run either process. This is called **deadlock**, and can happen on any kind of shared resources that require exclusive access. It can also happen with more than two processes, there could be three or more all waiting for the other.

Formal definition: A set or processes D is **deadlocked** if each process Pi in D is blocked on some event Ei, and event Ei can only be caused by some process in D.

Deadlock is only possible if certain necessary conditions are met, called the **Coffman conditions**:

1. Mutual exclusion - Only one process can use a resource at a time.
2. Hold and wait - A process continues to hold a resource while waiting for the other resource.
3. No preemption - No resource can forcibly be removed from a process holding it.
4. Circular wait - There is a circular chain of processes where each holds a resource that is needed by the next in the circle.

This is actually quite hard to avoid. If hold and wait never happens, e.g. a process is required to drop other resources it holds when it gets blocked, when it gets the new resource it will have to go back and pick up the other resources again. This may require it to drop the new resource while waiting, and it can easily get into a situation where the process never manages to get all the resources it needs. This is called **indefinite postponement**.

There are two approaches to the problem of deadlock:

1. Prevention - Stopping it from every happening by preventing one of the conditions from occuring.
2. Detection and breaking - Letting deadlock happen, but spotting it when it does and then breaking it by destroying one of the conditions.

Prevention can be broken down further into:

1. Prevention - Constrain resource allocation to prevent at least one of the conditions (e.g. ensure hold and wait never happens).
2. Avoidance - This is even more careful not to allocate a resource that it can be determined that might possible lead to a deadlock in the future. Avoidance is harder to manage, but tends to be more efficient on the use of resources than prevention as it avoids bad computation paths earlier.

Breaking any one of the four Coffman conditions would make deadlock impossible. Mutual exclusion can't be broken without a change in the architecture, because resources such as disks only have a single read-write head which can't be shared between two processes. The architecture change required to break mutual exclusion is the use of **virtual devices**, such as print spooling.

Hold-and-wait can be broken by requiring a process to drop all of its held resources if it becomes blocked on another resource. This is inefficient, as it might take a long time for all of the necessary resources to become available at the same time. A variant of this is for a process to request all of the resources that it could possibly need and block until they are all available. The problem with this is that a process could carry on doing useful work until it needs a resource, which is impossible in this system because the process can't start until it has its resources. It's also possible for a process not to know what resources it will need ahead of time.

No preemption can only be broken for certain kinds of resources, whose state can be saved and restored. This is because if a resource is taken from a process through preemption then it must be returned to that process in exactly the same state it was left in. For instance, if memory was written to, taken away, overwritten and returned, the first process would think its data was still in memory. Some resources can have their states easily saved, making preemption possible.

Circular waits can be resolved by assigning an order to resources, and requiring that processes must request resources in this order. If a process needs a resource lower down in the order, it must drop all higher-ordered resources, pick up the new one, and then pick up all the ones it dropped. This can be inefficient, and attempts to increase its efficiency usually reduce to processes requesting all of their resources at once.

Deadlock avoidance doesn't try to stop one of the conditions, but tries to determine whether each resource allocation will possibly lead to deadlock in the future. Requests deemed unsafe will not be granted by the OS.

The **Banker's Algorithm**, proposed by Dijkstra, uses two tests to see whether an allocation might result in deadlock. It tests for **feasibility**, whether the request is possible, and **safety**, whether the request can lead to deadlock.

The feasiblity test is easy - it passes if, after granting the request, the allocated resource is not more than the total resource. The safety test passes if there is at least one sequence of allocations and releases by which all processed can complete. Only requests which are both feasible and safe are granted.

For this algorithm to work, for each process the OS needs to know the current allocation of each resource, and the maximum possible allocation of each resource. Problems with this algorithm are
- There must be a fixed number of resources to allocate
- The process list must remain fixed, new processes cannot join
- Processes must know their maximum needs for each resource in advance
- The safety test is expensive to compute
- Requests can be refused that could have completed without deadlock, meaning resources are idle

Deadlock detection be done using **resource request and allocation graphs**, or RRAGs.  
![](http://gyazo.com/fb577ecd8ec71f7240f46815ed676dec.png)  
This shows process P1 requesting resource R1, and resource R1 being currently held by process P2. P1 is blocked. When deadlock occurs, this diagram will form a circuit:  
![](http://gyazo.com/4f692e9f37cb7d9309c962ef745e115a.png)  
Deadlock detection involves finding these circuits in RRAGs using a process called graph reduction. This is done by removing all request links for available resources, then removing all allocated links from resources to the process.

Deadlocks can also be broken by detecting pairs of processes which have been blocked for a long time, and killing one or both of them. Determining which processes can be safely killed isn't trivial.

In real life, prevention and virtualisation are used to prevent deadlock. With virtualisation, each process believes it has sole access to a resource, but actually it only has access to a virtual resource which will be translated to an action on the real resouce by the OS. This process is called I/O scheduling.

**Priority inversion** is where a low-priority process can deadlock with a high-priority process. The low-priority process is then preempted for its other resources by medium-priority processes, meaning the high-priority process is indefinitely postponed.  This can be fixed with **priority inheritance**, where the low-priority process inherits the high priority of the process it is blocking until it can complete. Alternatively, **priority ceilings** are assigned to each resource, and any process holding that resource has its priority temporarily boosted to the ceiling of that resource.

####Process Protection

By forcing access via the kernel, we ensure that one user cannot interfere with the processes of another user, therefore a process must include the notion of a user. This is usually encoded as a unique integer, the *userid*, which the OS uses to determine whether one process can access files, other processes etc. It is also used in Fair Share scheduling. Many resources have a userid associated with them, e.g. chunks of memory and files, telling the kernel which processes can access it.

A new process usually inherits the userid of its parent process. This leads to another bootstrapping problem of how a user can get a process running in the first place. To solve this, there is a distinguished user (can be called the superuser, root or administrator) - this is a normal user, but the OS allows it full access to other users files, processes etc. It can also suspend or kill any user's processes.

The root user is not to be confused with kernel mode. Root's processes run in user mode, just like other user's processes, and hardware access is still mediated by the OS. The difference is that the inter-user protections are not enforced by the OS. Privilege seperation between the superuser and normal user is used for protection of OS resources in exactly the same way as kernel mode and user mode is used for protection of hardware resources - same idea, different contexts.

Root can change the userid of its processes, giving away its privileges but thereby allowing a normal user to have a process. When a user logs into a system, a process (owned by the root) starts up, changes its userid to the user, and then starts other processes as that user - this solves the bootstrapping problem.

Many resources are restricted so only the superuser can use them. This provides an extra level of protection to resources that are sensitive. For example, we can't allow any user process to shut down the computer, so this operation is restricted by the kernel to the root user. Any shutdown program will need to gain root ownership, and will be carefully policed by the system.

The root is generally trusted by the kernel, meaning root processess can completely trash everyone's programs and data on the machine if they want to. This is why you should keep the use of the administrator account to a minimum, as doing everyday stuff as an administrator is asking for trouble.

This user-level protection is what prevents one user's processes intefering with another user's, as they have different userids so are kept seperate by the kernel. This means if one user accidentally downloads a malicious worm or virus, the damage is limited to just that user's files and processes - not ideal, but better than letting it have full reign over the whole machine.

A big reason for the spread of malware in Windows is that too many programs run as administrator, which can cause the whole system to be be affected if the program contains malware. If an OS *requires* the use of a virus checker, this is a sign that the OS isn't confident in its implementation of process protection. Virus scanners address the symptom, not the problem.

####Capabilities

Root access is a bit all-or-nothing, as it allows root all access to all resources. A refinement of the root idea is *capabilities*, which break access rights down into small parts e.g. right to access the network driver, access the filesystem, reboot the computer etc. This can be broken all the way down to rights to access individual files. These rights are called capabilities, and are like tokens that can be passed around and inherited by processes.

They allow finer control of security at the cost of a more complicated checking system. A few OSs, notable Flex, were built around the notion of capabilities and required hardware support to make things work with an acceptable speed - however, these never really took off. The idea has come back to modern OSs however. When Android installs an application, it asks the user whether that application should be allowed to access various system resources e.g. WiFi network access, phone contact list access, initiate phone calls etc.

Android calls these permissions rather than capabilities. It means that when an application runs, it can only access the resources the user has approved. This mechanism would be great if the user could be trusted to read and understand the list of requests, or was able to deny individual permission requests.

####Inter-Process Communication

Many processes can be created, process then exit without needing to refer to any other process, but there are many processes that need to send data to or receive data from other running processes. For example, a new program starting might wish to tell the process managing the display that it wishes to pop up a window on the display. Or, one process may have to wait for another process to finish some action (e.g. pop up a window) before it can progress itself - this is called *synchronisation*.

IPC can be achieved in many ways, but it must be supported by the OS, because by default the kernel tries to stop one process interfering with others. IPC contradicts this non-interference, so there must be rules and restrictions, or else one process could just blast another process with data, preventing it from doing any useful work.

######Files

The simplest way for two process to communicate is using an existing resource, namely files. Process A wishes to send some data to process B, so A writes it to a file and B reads it from the file.

There are issues however - which file to use? A and B need to agree on a filename to use. They can use a single "well known" file, but this is problematic if many processes are all writing to the same file simultaneously. They could have a seperate file for each pair of processes, but to agree on a file name A and B must have previously communicated.

Also, how can B know when data has arrived? It might have to repeatedly poll the file until the data arrives, which doesn't scale well to large numbers of files or processes. The file protections must also be set properly (with userids) to allow only the authorised processes to read and write to them.

Files are quite slow relative to other IPC mechanisms, and in general aren't used for IPC. However, they should be considered as a choice when *huge* amounts of data need to be transferred.

######Pipes

A pipe connects two processes together, taking output from one and feeding it as input to the other.  They have a fixed size: 4096 bytes is common. A writes to the pipe and B reads from the pipe independently of each other, like with files. Bytes are read out in the same order they were written in (FIFO). Unlike files, pipes also provide elements of coordination and synchronisation.

If A tries writing to the pipe when it is full, or B tries reading from the pipe while it is empty, the process is blocked by the OS until space has been freed up by B reading some or until bytes are available by A writing some. Thus the scheduling of A and B will be affected.

The pipe is implemented as a buffer held by the kernel. Every write to or read from the pipe involves a syscall - this is how the kernel can control blocking A and B, making sure A does not overfill the buffer and making sure B is not reading data that is not there.

Implementation of a pipe:  
![](http://i.gyazo.com/225a66d5c853a8069337b72666ce5c71.png)  

Pipes are supported well by Unix and are very easy to create and use from a shell. For example, if I were to write "% ps | sort". % is the shell prompt, ps is the list processes command, | is the notation for a pipe and sort is the sorting program. So this would create a pipe between the process listing program and the sorting program, meaning the list of processes is the input to the sorting program, so it would produce a sorted list of processes. I could also write "% gendata | sort | uniq" - gendata is a user program that generates some data, sort sorts it, and uniq removes duplicates, so this produces a list of the unique lines in the data.

A typical sequence in a program is for a process to create a pipe then fork a child process. The pipe is now ready to use for IPC between parent and child.

Pipe advantages:
- Simple and efficient
- Easy to use from programs and from a shell
- A powerful way of combining processes and programs
- Used a great deal

Pipe disadvantages:
- Unidirectional
- Are only between related processes. Often one is the parent of the other.
- Can create deadlocks if used carelessly (A creates a child process B with two pipes A->B and B->A)

Pipes are so useful that there have been a couple of extensions to them. *Named pipes* can be shared by unrelated processes, and *sockets* are pipes between processes on different machines, and are the basis of the Internet.

######Sockets

A socket allows bidirectional IPC between two processes (remember pipes are unidirectional). The processes may be on the same or widely remote machines. The technical issues behind implementing sockets are much more complicated than basic pipes, but they present the same kind of FIFO, byte oriented blocking channel for communication.

######Shared Memory

In early computers, all memory was shared between processes - one process could easily write to the memory allocated to another process. One process could easily write to the memory allocated to another process (this is generally a bad idea, so is now prevented by the kernel with MMUs). However, access to memory is very fast, so can be useful for IPC. This goes against the original purpose of an OS, so must be carefully controlled.

Like files, we have the issues of:
- Which area of memory to use? A well known area, or per-process areas?
- How does B know when data has arrived? Memory is always there, unlike files which can be created and removed, so when polling memory it can be hard to know if you are reading the data you want or some junk that happened to be lying around. A might write a special value to a specific memory location to flag that the data is complete, but again B must poll this location to see when this is done.
- The memory protections must be set properly to allow only the authorised processes to read or write it.

The speed of shared memory makes it very good for IPC, particularly large chunks of data, as long as it is supported by further mechanisms like signals or smeaphores to flag when data is ready.

######Signals

A signal is a software equivalent of a hardware interrupt, and can be sent (initiated/raised) by the kernel or a process. When a process receives a signal, it stops what its currently doing and goes off to execute a signal handler, just like a hardware interrupt with interrupt handlers. This all happens within the user program - the signal handler is just some specific code in the program, written by the programmer.

When a signal is raised, the process is preempted (if it was running) and the OS takes over. If the process wasn't running, the OS just notes the signal in the process, and when the OS next runs the process it jumps to the signal handler code within the process, rather than to the place where the process was preempted.

A process can send a signal to another process (or even itself) that has the same userid. The normal userid restrictions apply here - only root can send a signal to another users process. Naturally, the kernel can send signals to any process. The POSIX function kill() is used to send a signal in a user program.

A signal is just a single bit, but there are many different types of signal (HUP, INT, KILL, PIPE etc). A process can, to some extent, choose how to react to a signal. It can:
- Ignore it
- Accept it and act on it, i.e. run the signal handler code
- Suspend (voluntarily relinquish)
- Terminate

There are some signals which cannot be ignored, particularly the KILL signal, which will always terminate the process. This is why signals are regulated by the kernel; a user can kill their own processes, but not others.

Signals are *asynchronous*, meaning they may arrive at any point during the running of the program. Programs that use signals must be written accordingly, as they may arrive at inconvenient times. There exists default signal actions for each type of signal, but a program must include its own handler functions if it wants to do something other than the default action when it receives that signal. When a signal is received, the process stops what its doing, saves it's state and calls the signal handler. If and when the handler exits, the process continues from where it was interrupted.

Here are some example signals:
- INT - A general interrupt. Ignorable.
- ILL - Sent by the kernel to a process when it has tried to use a privileged (or non-existent) machine instruction.
- KILL - Non-ignorable terminate.
- SEGV - Sent by the kernel to a process when it has tried to access memory it shouldn't.
- ALRM - A timer signal.

Signals are:
- Fast and efficient
- Used a very great deal
- Only transmit a small amount of information, so often are used in concert with other IPC mechanisms
- Are a bit fiddly to program correctly.

######Semaphores

The action of process A waiting for process B to finish something before A can continue is very common, e.g. waiting for data to be written to an area of shared memory. Signals can be used for this, and are appropriate when you want to continue computing on something else. An alternative is to use a semaphore, which is used for waiting.

Invented by Djikstra, a semaphore allows *mutual exclusion*, where we can be sure only one process is accessing a resource at once. A semaphore is a variable whose value can only be accessed and altered by two operations, V and P. There are many alternative names for this; signal and wait, post and wait, raise and lower, up and down, lock and unlock etc.

Let S be a semaphore variable, usually residing in a chunk of shared memory, and start with S=1. P(S) sets S=0 if S=1, otherwise it will block on S. V(S) checks if one or more processes are blocking on S, and allows one to proceed if there are. Otherwise it sets S=1. So if another process wants to use the resource, it has to wait until the first process has done a V to signal the resource is ready. These operations are atomic, meaning there is no gap between the tests and the actions.

If multiple processes attempt a P(S) simultaneously, only one will succeed and continue, and hte others will be blocked. So if we had the code 'wait(S), some code, signal(S)' being run by multiple simultaneous processes using the shared semaphore S, only one process can execute the code at a time. The others will be blocked and get their turn later. Generally this code would be to access some shared resource (often shared memory, e.g. B shouldn't read until A has finished writing), so the semaphore makes sure only one process can access the resource at a time. The protected code is called a *critical section* - it is critical that only one process runs it at a time.

The previous example used a *binary semaphore*, as it takes just two values, 0 and 1. An alternative is a *counting semaphore*. Start with S=n. P(S) sets S=S-1 if S>0, else blocks on S. V(S) checks if one or more processes are blocking on S then allows one to proceed, else sets S=S+1. This system allows no more than n processes into the region at once.

Semaphores were first used within OS kernels to protect shared resources, but can be used in user programs to protect resources there too, e.g. a chunk of shared memory.

Correct implementation of user mode semaphores is very hard. The code above won't work as a semaphore because there is a gap between the testing and setting, which could lead to problems if:
- The process is rescheduled in the middle between the test and the decrement of the count.
- There are multiple parallel processors accessing the semaphore simultaneously.

This can be solved using hardware. Some CPUs have a test-and-set instruction, which can test and set a value on a register or memory location atomically, eliminating the gap between the two. We can use test-and-set to protect critical regions. However, not all makes of hardware support test-and-set, so it is better to use semaphores that can be implemented in other ways.

Another hardware solution is an atomic instruction to exchange the values of two variables v and w, e.g. 'temp=v; v=w; w=temp;'. This too can be used to build a semaphore. If you are using a machine that does not have such hardware instructions, there are several algorithms that build an atomic semaphore out of non-atomic operations.

Advantages of Semaphores:
- Each semaphore only needs a few bytes of shared memory
- They are small and fast given hardware support
- Used in both OSs and user programs to protect critical resources
- Are widely available in POSIX libraries

However, semaphores are a very low-level mechanism and can easily cause deadlock. If two processes each grab semaphore protected files, then each tries to grab the file grabbed by the other, both processes will be blocked. Some regard semaphores as too low-level and easy to misuse, so there are many other operations that have been devised to provide synchronisation and mutual exclusion:
- Condition Variables - More synchronisation than mutual exclusion. Allows processes to agree on when to proceed.
- Barriers - To synchronise a number or processes at one point.
- Monitors - More 'object oriented', as blocks of critical region code are implicitly protected (as provided by Java).
- ...and more where the construct tries to hide the complexity of synchronisation from the programmer (tuple spaces etc.)

######Application Level

IPC at the application layer uses high level mechanisms for passing data between processes. As always, this goes via the kernel (often using one of the other mechanisms e.g. pipes or shared memory with signals or semaphores), but uses high level constructs so we as programmers don't have to worry about the details. These are always implemented by system libraries and a fixed interface presented to the programmer regardless of the underlying implementation.

Popular implementations include CORBA, DCOP, Bonobo, D-Bus, COM and others. These try to be language independent, with each language having a set of bindings (standard functions) to access them. They focus on passing objects between components, so they need a standardised method of representing the data/objects in a *message*. This is called *message passing*. These kinds of framework tend to be very complicated, as there are a wide variety of communications between a wide variety of components that they need to support.

All of these IPC mechanisms discussed can be used in tandem. For example a program might employ D-Bus to pass data from one application to another (e.g. cut and paste), D-Bus might use pipes to communicate between processes, the pipes may pass a filename between them, and the data is communicated in that file. The choice of which IPC mechanism to use depends on the application - is it a high or low level program? How much data needs to be communicated? What resources are available?

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

When designing multi-processor systems, one of the main problems is joining them all to memory. The disparity of speeds is magnified for every processor that is added, and a new problem is introduced called *cache coherence*. If a processor has its own cache, then these must be coherent - if one processor changes a value, it should also change for every other processor.

One solution to this is a *snoopy cache*. Each cache watches every other cache for updates and updates their copy of data to match. This is very complicated, very expensive and scales factorially with the number of processors in the system.

Commonly used solutions are *non-uniform memory access* (NUMA) where a certain part of memory is associated with one processor, and access by that processor to that area is faster. Processors can still access each other's memory, but this is slower.

Another solution is *distributed memory*. This is simple and uses message passing to send updates between processors. However, access to another processor's data is very slow.

In processor clusters, the limiting factor on the speed of programs is not the compute power but the memory access. Optimising the data placement can make a huge difference in how fast the program runs.

####Filesystems

Current technology has main memory being a few gigabytes, and is also *volatile* - the values disappear when you remove the power. To be able to handle larger quantities of data and to make it *persistent*, we use larger but slower devices, like disks. To organise this data, we need filesystems.

It should be noted that not all applications want to use filesystems. Some  may want to have direct access to the disk hardware in order to optimise it for their very specific needs, e.g. enterprise databases. However in general, mose people just want a simple, efficient way of accessing their data, which a filesystem provides.

Another thing to note is that a filesystem is just an organisation of data, and doesn't need to be associated with disks. Filesystems can be found wherever we have large amounts of data that needs organising; USB keys, iPods, phones etc. It can even be useful to have a filesystem on top of memory, as an organisational mechanism.

Also, the objects behind the filesystem don't need to store data. Reading from a file may actually be returning keystrokes from the keyboard, and writing to a file may actually be sending sound to the soundcard (this follows the Unix philosophy "all devices are files"). This makes accessing devices incredibly easy for the programmer - just read and write.

In the traditional sense of a file however, a *file* is simply a named chunk of data stored on a disk. Humans like easy names like prog.c, so there needs to be a way of converting these user-defined names to the place on disk where the data is stored. And when we have millions of files, we also have millions of names, meaning we need some way of organising these names. It is important to notice the distinction between the name and the data. The same name can refer to different data, and different names can refer to the same data.

Names are usually organised as a simple hierarchy. Rather than simply presenting all filenames to the user (a flat filesystem), names of related files are put together into a directory (folder). So a directory is just a collection of names of files. The names of directories can also be collected in other directories, and so on until we get to the top of the hierarchy i.e. the root.

Example of a filesystem:  
![](http://i.gyazo.com/efa9099520c60ae8e1e3e6b8fe08be70.png)  

Filenames can appear at all levels, but always within a directory. In many systems, a filename can be in more than one directory, while directories can generally only be within one directory. Directories can also be empty, containing no names.

The namespace heirarchy is useful becuase it makes referring to a file easy. For example, in Unix the path /usr/bin/ls refers to the file named ls, inside a directory named bin, insided a directory named usr, which is in the root directory. The root directory is referred to as /, though its actual name is empty. Other OSs have similar ideas, but may use different seperators like : or \. As previously mentioned, files can have multiple names - /usr/local/bin/dir may refer to the same file as /usr/bin/ls.

The directory hierarchy forms a *directed acyclic graphs* (DAG). This means there are no loops - we can traverse the whole hierarchy and never get stuck in a loop, and there will be no unconnected loops if we delete a directory. We might find the same file twice though, but this is a tradeoff of flexibility vs ease of sytem implementation.

Each process has a current working directory (cwd) which is stored in the process control block (PCB), so that whenever the process asks for a file by an incomplete filename (not starting with a /), the kernel glues the cwd prefix on to the given name and uses that instead. So if a process with a cwd of /u/cs/1/cs1abc asks for the file prog.c, it will get the file /u/cs/1/cs1abc/prog.c. This is how different processes can refer to the same name prog.c, but get different files. The cwd is a convenience for the programmer and may be changed as often as they like (cd, chdir etc).

Things we want to be able to do with a filesystem:
- Create a new file.
- Delete a file.
- Open a file to access it.
- Read data from a file.
- Write data to a file.
- Close a file when we are done.

Things we want to do with directories:
- Create a new directory.
- Delete a directory.
- Look through a directory for a filename or directory name.
- Add a file to a directory.
- Remove a file from a directory.
- Rename a file.

Some requirements of a filesystem:
- Speed of access.
- Speed of update.
- Scalability to large numbers of files.
- Efficient use of disk space.
- Reliability.
- Protection and security.
- Backup and recovery.

####Inodes

An inode is a fixed size structure stored on the disk, that contains the metadata of a file (all the information about it). The traditional Unix filesystem is based on inodes, and each file is described by one. Information in the inode includes:
- Timestamps - Dates and times this file was last accessed and last modified.
- Ownership - The userid of the owner of this file, for protection purposes.
- Size - How big the file currently is.
- Type - Whether this is a plain file, a directory, or some other kind of special file.
- Access permissions - Who can read or write or run this file, if it is a program.
- Reference count - The number of names this file has.
- A list of the areas on the disk where the actual data lives.

Filenames are *not* stored in the inode, they are stored in directories. A directory is essentially just a table of names of files and names of subdirectories, together with their inode numbers. Originally this was just a table, but these days use clever datastructures to manage the large number of names we use.

As inodes are a fixed size, it is easy to put them in a simple array on the disk and refer to them by their index in the array, i.e. their *inode number*. There can be multiple directory entries referring to the same inode, which is how a file can have many names. This means that a file cannot know its own name.

There are a couple of special names found in every directory. The name .. refers back to the parent directory, allowing us to climb up the hierarchy until we reach the root. So ../foo/bar.c is the name of a file in a sibling directory - up, across, then down in the hierarchy. Because there is nothing above / (the root), the .. of / is /. The name . refers a directory back to itself.

If the reference count in the inode (the number of names the file has) drops to zero, the OS can remove the file. Deleting a file is a matter of:
- Removing the name reference in the relevant directory
- Decrementing the reference count in the inode
- If the count reaches zero, we can free the inode and the disk block it refers to. There are freelists of inodes and disk blocks.

Each time a program opens a file, the OS increments the count, and decrements it when the program closes the file. So it is possible for a program to create a new file (reference count +1), open it (+1), delete it (-1), and it will still be able to read and write to it. The file will only disappear when the program ends (-1). No other processes can see this file, as there is no name in any directory that they can use to open the file.

The data for inodes is in *disk blocks*, which are fixed size areas on the disk e.g. 512 or 1024 bytes. Having a fixed size allows for easy and fast allocation and deallocation. Files are always allocated a whole number of blocks, but this can lead to wastage. For example, a 1025 byte file might need two blocks, but uses just one byte in the second block. However, there are lots of tricks in real filesystems to avoid this.

An inode is of a fixed size, so may have space for say 10 block pointers. If each block is 1024 bytes, you can't have files bigger than 10 x 1024 = 10KB. For files bigger than this, we use an *indirect block*, which instead points to an array of more blocks (it actually leads to an array of block pointers, which in turn lead to the blocks). This array may contain 256 blocks, which is 256KB more space. Bigger files may have a *double indirect block*, which leads to an array or indirect blocks, which each lead to an array of blocks, so a double indirect block with array size of 256 would give us 256 X 256 = 65536 more blocks, which is 65MB more space. Extremely big files need a triple indirect block, which is an array of double indirect blocks, giving us 256^3 blocks - around 16 million, which is 16GB more space.

The multiple indirects system has recently re-emerged in a new filesystem F2FS, the 'flash friendly filesystem'. Devised to match the peculiarities of modern flash memory-based storage (SD cards etc.) it uses this less time-efficient but more update-efficient approach. It targets systems which currently use FAT, microsofts more simply but somewhat clunky filesystem.

This multiple indirect approach seems wasteful, as every indirect block is overhead occupying space on the disk. However in practice it's not too bad, as most files are quite small and don't need them, and the relative overhead for large files is pretty small too.

Reading through the inode and indirect blocks from disk every time a file is accessed is quite time consuming, so a typical OS will read them just once and cache the inode and the indirect blocks in memory to reduce the lookup overhead. If they are modified, the OS will periodically write them back to disk. A good Os will even keep copies of the disk blocks in memory too, so reads/writes to disk are just reads/writes to the in-memory copy. The OS will occasionally write the blocks back to disk, whenever it is convenient to do so. This is why you shouldn't just pull a out a USB stick, as the in-memory copy of the disk may well be out of sync with what is on the actual device. The 'safe to remove' is an indication that everything has been synced up.

The space in the inode for the disk block pointers is used for various other things when the inode refers to something other than a disk file. For example, a *soft link* (similar to a Windows shortcut) to a file or directory. This is a special inode who's purpose it say "don't look at me, look at this other file instead". A flag in the inode header tells the OS that this is a soft link, not a reference to a file.

The contents of a soft link is just the name of the inode for the file it redirects to. For example, the contents of a soft link named /home/foo that linked to /mnt/bar would just the string "/mnt/bar". When a program opens foo, it is the job of the OS to not present the data "/mnt/bar", but to close the inode referred to by foo and open the inode referred to by bar, and return the data it finds there instead.

A hard link is the normal reference to the inode of a file, while a soft link is an inode which acts as a signpost to another inode. An important difference is that the soft link might conceivable point to a name that does not refer to an existing file, wheras the inode of a hard link *is* the file. And as there are no inode numbers involved in a soft link (just the name), it can be the name of any file on any filesystem, even a filesystem that is not based on inodes.

When a program opens a file, the OS must find where on the disk the file lives, which means finding the blocks on the disk that contain the data of the file. Say we are looking for the file prog.c with a cwd (current working directory) of /home/rjb. The process goes like this:
- The name prog.c is incomplete, so the OS prepends the cwd giving the full path /home/rjb/prog.c
- The Os reads the blocks containing the root directory from the disks, and scans through for the name home. It finds it, gets the inode number for home, reads that inode from the disk, and finds that it refers to a directory.
- It reads the data block containing the home directory from the disk, and scans it for the name rjb. It finds it, gets the inode number for rjb, reads that inode from the disk and finds it also refers to a directory.
- It reads the data block containing the rjb directory from the disk, and scans it for the name prog.c. It finds it, gets the inode number for prog.c, reads that inode from the disk and finds it refers to a file.
- It can now read the data blocks containing the file from the disk.

This process must be repeated for every file opened. Caching copies of the inodes and directories in memory rather than re-reading them from disk every time speeds up the process greatly.

If we want more than one filesystem, or more than one kind of filesystem, we can split the disk into seperate *partitions*. A partition is just a section of disk owned by a single filesystem. So we can have multiply filesystems on a single disk, e.g. two Unix filesystems and a Windows filesystem. Each filesystem has its own inode tables (or whatever it requires) and are logically quite seperate. However, inode 23 on one partition is different to inode 23 on another partition, so we can't have hard links across partitions. We *can* have soft links across partitions though, as soft links are by names, not inode numbers. This is really why soft links were invented in the first place.

Under Unix, a filesystem can be *mounted* on another filesystem. A *mount point* is a note to the OS that says "stop looking at this partition and look at that partition instead".

![](http://i.gyazo.com/8b71fddb100dd7786a767b3018d2d4f8.png)

In filesystem A, the filename /usr/local/bin/prog refers to the prog on A. If we mounty filesystem B at the mount point /usr/local however, this hides the part of the hierarchy below.  /usr/local/bin/prog now refers to the prog on B. When the file lookup gets to the mount point at /usr/local, it switches filesystem and continues looking from the root of B. The benefit of this is that we can have many partitions presented as a single unified filespace, with a single unified namespace for files. Partition B could be on a seperate disk, or a USB key, or a read-only medium like a CD, but to the programmer it's just one big filesystem. This unified namespace is completely different from Windows, where each partition has a prefix like C: or D:.

B will still have it's own inode table, so there can't be hard links between the two partitions, as inode numbers always refer to the inode table in the current partition we are examining. B may even have a completely different kind of filesystem which doesn't use inodes, or could be on a seperate machine if this was a mount of a network disk. Also, in Unix the thing behind the filesystem interface might not even be data files on a disk, it could be a HTTP filesystem where files are web pages for example.

On the flip side to this, there are mechanisms for gluing several disks together to make them appear as a single partition, which can be useful for making huge filesystems out of small disks, or for reliability through redundancy (RAID).

####Operating Systems

Operating systems are still a current topic of research. Low-power systems for mobile devices are still relatively young, and OSs are still being developed for very large machines too.

*OS virtualisation* is important with cloud computing. Many users are sharing the same hardware but each has their own private OS running their applications. OSs were the software closest to the hardware, but this isn't true with virtualisation.

*Bare metal virtualisation* uses a thin layer called the *hypervisor* between the OS and the hardware. Each OS sees a different virtual machine which it has full control over.  
![](http://i.gyazo.com/e82c07f94190a0fc2f4b64b00bac3ff3.png)  
The operating systems can be completely different.

*Hosted virtualisation* has a host OS that runs virtualisation code on which other OSs run. This is how virtual machines such as VMWare work.  
![](http://i.gyazo.com/bff71ddf611e1ca4935b8390b9d55741.png)

*Containers* are not strictly OS virtualisation, instead giving each application a rigid partition in which to work. Applications can't see or influence what happens in other containers.  
![](http://i.gyazo.com/5b154fdd0f1e7dd82a37c7e2b209d444.png)  
The applications must run on the same OS, but they can have different system libraries and environments.

*Hardware virtualisation* is where the OS emulates a type of hardware that it isn't necessarily running on. For instance, an X86 computer can emulate an ARM chip. These emulations are slower than native hardware, but allow for flexibility and ease of testing.  
![](http://i.gyazo.com/4b517d66b94fa4b2f24880ea55dedf17.png)  

###Networks

###Networks History

The "Internet" (capital I) is the world-wide collection of networks. An "internet" (lowercase i) is an abbreviaton of "internetwork", which is just some collection of networks. An "intranet" is some collection of networks belonging to a single organisation. *The Web is not the Internet*.

The internet started as a project by the American Advanced Research Projects Agency (ARPA) in response to the Russians launching Sputnik (the first sattelite) during the Cold War. The idea was to connect the Agency's expensive resources, namely their computers, allowing them to be shared. The design was to be non-centralised to avaoid single points of failure, particularly nuclear attacks, so it was designed to have multiple paths between hosts.

Using simple circuits between machines would be too vulnerable, so *packet switching* was invented. Data is chopped into small chunks (i.e. packets), and each packet is sent individually, possible over different paths. The original data is then reconstructed at the receiving host.

This causes a few problems though. How is the data split? How are the routes found? How do we reconstruct the data from the packets? A packet doesn't know how to get to it's destination, and neither does the source host (unless it's on a local network). A packet is like a postcard with the address written on it, it relies on the *routers* it passes through to make the right decision.

To ensure maximum interoperability, the internet relies on standards and defined protocols. The use of standards means that two machines will be able to communicate with eachother, even if they are made my completely different companies, are of completely different techonologies, and have never previously interacted.

###Layering Models

To make two computers communicate, we need some hardware to cnnect them, so there must be some kind of electrical (or other) thing between them. They must then be compatible on voltages, how bits are represented as electrical or optical signals etc., and must agree on how to represent data as bits, e.g. signed or unsigned integers.

To implement a network system, we need to follow a sensible structured standard. Designing a standard like this is too big a problem to tackle all at once, so the design is split into layers, each with a well-defined functionality. A *layering model* for a system is a suggestion on how to split up the design - it is *not* a networking standard, but a recommendation on how to approach the design of the standard. After you have the standard, you can then make implementations based on the protocols the standard provides. To summarise:
- We pick a layering model
- We use this to guide us in making a standard
- The standard will specify various protocols
- Implementations will then follow and excute the protocols

It is very important that the protocols are documented clearly, so that implementations can follow them precisely without ambiguity or omission. Protocols include the expected interactions and interchanges between the entities (hosts) concerned, the messages involved, the message formats used, the actions expected of the entities etc., all so that the entities can agree on something. For networking purposes, this is that some data has been safely passed from one entity to another.

There are two main layering models in use for networks, the *ISO Open Systems Interconnection (OSI) Seven-Layer Model*, and the *Internet Four-Layer Model*. The OSI model is widely used in courses on networks, while the Internet model more closely resembles how things are done in the real world.

Layers should be:
- Easy to implement
- Represent a well-understood concept or abstraction
- Must only interface with its neighbour layers
- Chosen so that the meta-information flowing across boundaries is minimised

A layer must be as self-contained as possible and disregard all other layers as far as is possible, i.e. *modularity*. With modularity, an implementation of a layer can be removed and replaced without affecting the overall system.

There are 7 layers to the OSI model:

1 - **Physical layer**. This is the hardware layer, and deals with the transmission of bits over a channel. It handles things like what voltages/colours of light pulses/radio wavelengths to use, what encoding for bits, how long (in time) a bit should be, how many wires to use in a cable, what plugs to use on the cable... and much more. Generally, anything to do with choices regarding hardware.

2 - **Data link layer** (also called the *media access layer*, or MAC). This takes the physical layer and tries to create a channel where there are no undetected errors of transmission - we know that networks are not 100% reliable, so we must take into account the possible errors and deal with them.

A typical MAC layer sends the data as a sequence of frames, which are chunks of bytes, maybe tens of thousands of bytes long. If a frame is corrupted, the MAC layer may resend it, or maybe there is enough redundancy in the bit encodings to fix the error. Some link layers do this, while others just do nothing at all, letting higher layers figure out whats gone wrong and find a solution.

3 - **Network layer**. This layer controls the operation of the network, particularly the issue of *routing* data from source to destination. It can also deal with *congestion* - when there is too much data for a particular link, it might route some data via another link, or use *flow control* to slow down the rate of transmission. Alternatively if things are going well, flow control is used to speed up the rate of transmission.

4 - **Transport layer**. This accepts data from the session layer, and arranges it into packets suitable for the network layer, i.e. *packetisation*. In the other direction, it takes packets from the network layer and reassembles it into the original data stream, i.e. *depacketisation*. This will need to deal with packets arriving in a different order than they were sent.

5 - **Session layer**. This layer manages sessions between source and destination, for example a remote login session. Sessions can be quite short, e.g. just long enough for an email or web page to be transmitted, or arbritarily long. In general, a session is just some logically cconnected set of exchanges that have some unified identity, e.g. if the network crashes and reboots halfway through a big data transfer, the session can be picked up from where it left off, rather than starting again.

6 - **Presentation layer** - This provides a few things so that we don't have to reimplement them in every application. In particular, it decides on representations of data, such as characters, integers and floating point values. This means the source and destination can agree on how a particular stream of bits should be interpreted. So if the source wants to send the number 7, the presentation layer deals with encoding this in a suitable way, e.g. as some particular bits, and allows the destination to realise that this particular sequence of bits represents the number 7.

7 - **Application layer** - This is the only layer that most programmers see. It contains protocols like HTTP for the Web, SMTP for email, and so on. Built on top of these protocols are the applications that the users see, e.g. Firefox for the Web or Pine for email.

Remember - **People Don't Need To See Pink Alligators**. Sort it out, people.

Conceptually, data from an application is passed down through the layers until it reaches the hardware. As it passes from layer to layer it is *encapsulated* - a transformation of the data in such a way the the layer below can cope with it transparently, and in a way that it can be untransformed back again. At each layer, the transformation might:
- Add an identifying header or trailer (or both) that is needed for the functionality of the layer
- Encode certain bit patterns that might be misinterpreted or mis-transmitted by the next layer
- Put items in a standard form e.g. integers into a well-known format
- Do some arbritarily complicated manipulation
- Do nothing

Here is a diagram showing a possible (but unlikely) OSI encapsulation.          
![](http://i.gyazo.com/29f915a67e32e2068dbc75adb83a368e.png)

An example of this is early modems which treated bytes values less than 32 as commands instead of data, e.g. 4 might mean 'end transmission' instead of the number 4. You simply can't send the value 4, as the modem would interpret this as a command and end the connection. This means you need to transform the data somehow so that 4 is never seen by the modem in the datastream. This transformation must be reversible, so the other end can reconstruct the four. This is why encapsulation is necessary - so that data can be transmitted accurately, even if you are using weird hardware.

In this situation, the transformation used was often *byte stuffing*. The link layer could replace "04" by, say, a pair of bytes "DB D4". The link layer ar the other end could recognise this pair and replace it by the single byte "04". The "DB" here is called escape character, and it's presence in the datastream means the next character is encoded, so special action must be taken. If the escape character appears is in the datastream, that needs to be stuffed too, e.g. "DB" may become "DB FF". Using escape characters means there is less space for data, so byte stuffing is a tradeoff between some expansion of the data and correct transmission of the data.

A similar situation is telephone phreaking, where sounds made down a telephone were misinterpreted as commands to the telephone exchange. The problem here is that the same channel is being used both for the data and the control of the data - each can be mistaken for the other unless care is taken.

As far as the different layers in the model are concerned, they don't know exactly what the data they receive represents. They simply transform it somehow, maybe prepend a header to indicate the kind of transformation used, then pass it to the next layer. When sending data, it travels down through the model being transformed at each stage, until it reaches the physical layer where it is transmitted. When receiving data, it proceeds up the layers, unwrapping and untransforming at each one, until it we get the original data reaching the application (hopefully).

All these headers and encapsulation may seem wasteful however, as if the data is small then the data transmitted on the wire may be mostly headers and footers. However, it gives us *flexibility*, meaning we could replace the 1Gb network card in our machine with a new improved 10Gb network card, and because the physical layer is totally seperate from the data link layer, we can write an implementation for the new 10gb physical layer, and slot it in where the old one was without the other layers knowing anything has changed.

**The Internet model** is a four layer model, developed after the Internet Protocol had gained popularity. The primary implementation of this model is TCP/IP, but that is the instance, not the model. They are often confused because they seem so similar, however it is possible (although unlikely) that a network protocol other than TCP/IP could be based on the four layer Internet model.

1 - **Link layer**. This corresponds to the physical and data link layers in the OSI model. The model doesn't say much about this layer, only that it has to be capable of sending and receiving Internet Protocol (IP) packets, so what you do with the hardware is pretty open.

2 - **Network layer** (also known as the internet layer). This directly corresponds to the OSI network layer, and handles the movement of packets, particularly routing. In TCP/IP, a protocol called the Internet Protocol (IP) is defined in this layer. It is an unreliable protocol, meaning it does not gaurantee the delivery of packets (sometimes it is better to deal with an occasional lost packet than to hold up the system while the lost packet is re-requested and resent, e.g. video streaming where fast delivery is more important than accurate delivery). 

3 - **Transport layer**. This directly corresponds to the OSI transport layer, and provides a flow of data between source and destination. In TCP/IP, there are two protocols in this layer - the *transmission control protocol* (TCP), and the *user datagram protocol* (UDP). TCP is a reliable protocol, making a reliable layer out of a potentially unreliable IP by a complex mechanism of packet acknowledgements. 

However, we don't always want to pay the non-trivial cost of that mechanism (e.g. in video streaming), so the other protocol, UDP, is not reliable. By not reliable, we mean it is as reliable as the underlying layer, IP. UDP was devised long after TCP, when it was realised how useful unreliable protocols can be, which i s why the protocol set is called "TCP/IP" - tht was the entire protocol set for a fair while.

4 - **Application layer**. This roughly corresponds to the OSI session, presentation and application layers. This means that Internet application programmers must take care over session and presentation issues. Many people forget this, e.g. historically some Web servers produced pages that did not display properly on other systems, because the programmers assumed all Web clients used the same data representations they used.

A typical email application will actually apply a presentation encapsulation *before* adding the application headers (To, From etc.). The Multipurpose Internet Mail Extensions (MIME) standard is a way to encode data (e.g. text, sound, pictures, video) in a safe way. It was originally developed in the context of email, but is now used in other areas like Web page delivery, where there are mixed kinds of data to transmit. Similarly for the session layer, if a persistent session is needed the application must code it, rather than it being something which comes built-in from another layer.

A typical implementation of TCP/IP has the following protocols:
- Link layer - Ethernet, Wifi
- Internet layer - IP and various control protocols (ICMP)
- Transport layer - TCP, UDP and others
- Application - HTTP, SMTP etc.

So the typical process to transmit an email over an Ethernet would be:
- The email application transforms the text using a MIME encoding (presentation)
- The email application adds an envelope header (From, To, etc.)
- TCP adds its header (reliability, packetisation)
- IP adds its header (routing)
- Ethernet adds a header (local routing) and a trailer (checksum)
- The bits are transformed using a 4B/5B encoding to smooth the bit patterns and are sent using a three-level electrical coding MLT-3 (physical)

A problem with the Internet Model (not TCP/IP) is that unlike OSI, which makes a clear distinction between model and implementation and is therefore general and can apply to many systems, the Internet Model is only good for describing TCP/IP.

####TCP/IP

The OSI model is widely used when teaching and thinking about networks, but protocols based on it are never used. The Internet model is rarely used but the TCP/IP protocol is based on it. The main reason TCP/IP is successful is that the standards are open so anyone can join.

Before the internet, networks tended to be closed and proprietary, and companies had to pay to become a part of the network. These failed to reach a critical mass, so when the TCP/IP standard came along it was the obvious alternative.

The Internet was initiated by ARPA, a US military department, but it was mostly developed in academia. Because this was a safe environment, the Internet was developed without regard for security, privacy or authentication.

By default, data in transit is readable by the machines it passes through, not protected from interference, and only weakly authenticated. These problems have been addressed through secure extensions to protocols, but these aren't always perfect.

Security and authentication through these protocols is added in the application layer, so it is the programmer's job to choose to use a secure protocol. This extra layer takes an insecure protocol (TCP or UDP) and makes it into a secure one through encryption and authentication.

Security can also be added to the network layer, which means it is implemented by the system rather than by the programmer and the user programs. This is harder to set up properly, and the computational overhead of cryptography is sometimes too high for system owners to use.

There are several popular hardware implementations, the most popular being Ethernet and WiFi. Ethernet was created in 1982 from the earlier Aloha protocol. It originally used *carrier sense multiple access with collision detection* (CSMA/CD).

CSMA/CD was used because Ethernet was originally a multiple access medium, meaning that several hosts use the same wire to send data. If two hosts tried to send data simultaneously, there would be a *collision*. This is where two electrical signals in the same wire would mix, making the data they represent unreadable. *Carrier sense* meant that the host listens to the cable before sending data, and if the cable isn't being used, they send the data.

This still isn't enough to prevent two hosts sending at the exact same time, so *collision detection* is needed. While sending, each host listens to the wire for collisions, and if one is sensed then both hosts wait a small random amount of time then retry the listening and sending. The random delay means a second collision is less likely, and it helps fairness between hosts.

*10Base5* Ethernet networks use *Vampire tap* connectors, and can run for a maximum of 500m without boosting.

*10Base2* Ethernet networks use *BNC* connectors, and can run for 200m.

*10BaseT* Ethernet networks use twisted pair cables and can run for 150m.

A *hub* is a simple electrical repeater that takes repeats all incoming signals on all outgoing wires. A *switch* is more intelligent, and only sends the signal down the wire on the path to the destination host. This requires a switch to read and understand the addresses in the packets and to know which hosts are plugged in to which sockets. Using a switch reduces the number of collisions.

An ethernet frame is split into:
- 6 bytes for destination address
- 6 bytes for source address
- 2 bytes for data type
- Between 46 and 1500 bytes for data
- 4 bytes for an error checking code  

These are layed out like so:  
![](http://i.gyazo.com/971d0396b310d8e9df02e5c294f42a00.png)  

The destination address will match up with the hardware address in the Ethernet card of one host. These addresses are unique. Every host can see every frame on its subnet, so hosts must read the destination of every incoming frame to check whether it is intended for that host. This is a security issue, because every host can also read data not intended for it.

This works well enough between computers on a local network, but if the destination isn't local then this approach would mean broadcasting our frames to everyone. This isn't feasible for scaling and security reasons. Also, this assumes that the destination host is part of an Ethernet network, which might not be true. Instead, we introduce *software addresses* and *IP*.

####IP

The network layer in the Internet Protocol is called IP. Its main function is to deal with the routing of packets. The packet header added by the IP has a hardware-independent network layer address, or an IP address. These are in the same format throughout the whole Internet:  
![](http://i.gyazo.com/fbccab14731dc794cc0202e1e564b67b.png)  

Source and destination IP addresses are four bytes long, typically written as four decimals. There is a structure in the IP address to help with routing: the first bytes (how many can vary) is the network address, identifying a network such as the University of Bath, and the last bytes are the host address, identifying a single host in the network.

This means that all packets destined for one network can be routed in the same way. Only when those packets enter the destination network is local knowledge needed. The host part is further split into *subnet* to help local routing within the university.

These addresses are independent of hardware, so they are the same on Ethernet as on WiFi or any other kind of network.

The problem now is that to send a packet, we need to know both the hardware address and the software address. Given a host's IP address, we need to find the corresponding Ethernet address. This is done by the *Address Resolution Protocol* (ARP). This is a protocol in the link-layer that broadcasts an ARP frame on the local network asking who has that IP address. The host with that IP address responds with its Ethernet address. These values are cached by each host, and expire in case a new machine takes that IP address.

This works when the host and destination are on the same network. If they aren't, the packet is instead sent to the gateway host and the process of non-local routing begins. In this case, the hardware address would be of the gateway and the software address would be of the destination host, two different machines.

The reason both hardware and software addresses are needed is because with non-local routing they refer to diferent things: the hardware address is for the next hop and the software address is for the ultimate destination. ARP isn't specifically for IP and Ethernet, it can pair and physical (hardware) and network layer (software) addresses.

####DHCP

When a machine is set up or turned on, it doesn't have an IP address. It uses the *Dynamic Host Configuration Protocol* (DHCP) to get one. When the machine is newly connected to a network, it makes a DHCP broadcast to the network, to which a special-purpose DHCP host must respond. This machine will read the request, choose an unused IP address, and send it back to the requesting host. The new host configures itself to use this address.

When a host is turned off, it is supposed to inform the server via DHCP that it is finished with the address so that it can be added back into the pool of free addresses. However, some hosts ignore this and sometimes it's impossible (eg in a powercut). This is solved by giving each address a lease time, after which the address expires.

If this expires while it's being used, the host can renegotiate use of the same address through DHCP. Lease times depend on the situation - for instance, in a coffee shop, hosts might only connect for tens of minutes, so this is a suitable lease time. In a data centre, the same hosts will likely be connected for months at a time, meaning long leases with little overhead can be used.

DHCP also supplies to new hosts the address of the gateway, the addresses of name servers (DNS), lease times, and the addresses of servers for things like printing and mail.

####IP Addresses

The problem with 4-byte IP addresses is that there aren't enough of them for all the computers - 2^32 is around 4.3 billion addresses, clearly not enough for a population of 7 billion. This 4-byte system is called IPv4, and is slowly being replaced by IPv6.

IPv6 replaces the network layer protocol with a new protocol using 16 byte addresses. This should have been a drop-in replacement, with the link and transport layers being unaffected, but mistakes made when designing TCP and networking APIs mean that mainstream use of IPv6 will probably not happen for a long time.

IPv4 and IPv6 do not interoperate, however they can both run side-by-side on the same physical layer. This will be the case until IPv4 is completely replaced, which might take a very long time.
