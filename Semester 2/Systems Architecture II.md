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

On the other hand, too frequent interrupts mean the monitor is forever being called and using CPU time, so less time is available for the progrums. This is another tradeoff - frequent interrupts for good interactive behaviour, or fewer interrupts for good compute behaviour. Therefore we need clever scheduling algorithms in the monitor to try to give high priority but small slices of time to interactive programs, and lower priority but larger slices to compute-intensive programs.

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

**Priority inversion** is where a low-priority process can deadlock a high-priority process. This can be fixed with **priority inheritance**, where the low-priority process inherits the high priority of the process it is blocking until it can complete. Alternatively, **priority ceilings** are assigned to each resource, and any process holding that resource has its priority temporarily boosted to the ceiling of that resource.

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

In early computers, all memory was shared between processes - one process could easily write tot eh memory allocated to another process. One process could easily write to the memory allocated to another process (this is generally a bad idea, so is now prevented by the kernel with MMUs). However, access to memory is very fast, so can be useful for IPC. This goes against the original purpose of an OS, so must be carefully controlled.

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

One solution 
