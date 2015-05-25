####1

1a - A set of processes D is deadlocked if each process Pi in D is blocked on some event Ei, and Ei can only be caused by some proccess in D.

1b - Mutual exclusion is when a resource can only be used by one process at a time.

Hold and wait is when a process continues to hold one resource while waiting for other resources.

No preemption is when no resource can be forcibly removed from a process which holds it.

1c - If we try to prevent hold and wait, by requiring a process to drop any resources it holds when it is blocked, this could lead to indefinite postponement - when a process never gets all the resources it needs, because when it gets one resource it will have to wait for the next, requiring it to drop the first. Also, preventing mutual exclusion would require a change in hardware, as some resources can only physically be accessed by one resource at a time e.g. disks with a single read/write head.

1d - Circular wait. This is when a circular chain of processes each holds a resource which is needed by the next process in the chain.

1e - Most modern OSs use a combination of prevention and virtualisation. Prevention is when resource allocation is constrained to prevent situations which could lead to deadlock, as this is easier than avoidance and efficient use of resources is less of a pressure these days. Virtualisation is where the OS pretends each process has sole access to a resource, but the data it writes to the resource is buffered by the OS somewhere, and sent to the resource when it's free.

1f - Partially. It solves the issue of deadlock, because every process can progress without waiting for the resources to become available, and the OS handles transferring the data to or from the real device. However this only creates a new problem, called I/O scheduling - when and in what order should the OS do each I/O?

####2

2a - A job is a collective word for the program and it's data, and would be prepared on paper tape before being given to operators to load and run them.

2b - Batch processing is when several programs are collected and loaded together in a single bunch.

2c - A language used to identify particular jobs to run and store their results. An example is JCL.

2d - Multitasking is loading more than one program into memory, meaning that if program A was doing something which takes a lot of time but doesn't use CPU, e.g. writing to disk, program B could run in the meantime.

2e - Cooperative multitasking is when an OS relies on processes relinquishing control to allow other processes to run, and was used before OSs had timer interrupts.

2f - Preemptive multitasking is when a hardware timer creates regular interrupts to return control back to the monitor, therefore enabling timesharing.

2g - Timesharing is when multiple processes share the CPU, and so appear to be running simultaneously.

2h - A timeslice is the amount of time that the monitor allows a process to run, e.g. a large timeslice means the monitor continued to schedule the process through multiple timer interrupts.

2i - Process scheduling is the problem of deciding which process to run next, decided by some kind of scheduling algorithm.

2j - Thrashing is when an OS spends more time deciding what to do and which processes to run than actually doing things/running them, and was a common problem for early OSs.
