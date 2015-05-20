#CM10195 - Systems Architecture
##Dr Russel Bradford

####Process Protection

By forcing access via the kernel, we ensure that one user cannot interfere with the processes of another user, therefore a process must include the notion of a user. This is usually encoded as a unique integer, the *userid*, which the OS uses to determine whether one process can access files, other processes etc. It is also used in Fair Share scheduling. Many resources have a userid associated with them, e.g. chunks of memory and files, telling the kernel which processes can access it.

A new process usually inherits the userid of its parent process. This leads to another bootstrapping problem of how a user can get a process running in the first place. To solve this, there is a distinguished user (can be called the superuser, root or administrator) - this is a normal user, but the OS allows it full access to other users files, processes etc. It can also suspend or kill any user's processes.

The root user is not to be confused with kernel mode. Root's processes run in user mode, just like other user's processes, and hardware access is still mediated by the OS. The difference is that the inter-user protections are not enforced by the OS. Privilege seperation between the superuser and normal user is used for protection of OS resources in exactly the same way as kernel mode and user mode is used for protection of hardware resources - same idea, different contexts.

Root can change the userid of it's processes, giving away its privileges but thereby allowing a normal user to have a process. When a user logs into a system, a process (owned by the root) starts up, changes its userid to the user, and then starts other processes as that user - this solves the bootstrapping problem.

Many resources are restricted so only the superuser can use them. This provides an extra level of protection to resources that are sensitive. For example, we can't allow any user process to shut down the computer, so this operation is restricted by the kernel to the root user. Any shutdown program will need to gain root ownership, and will be carefully policed by the system.

The root is generally trusted by the kernel, meaning root processess can completely trash everyones programs and data on the machine if they want to. This is why you should keep the use of the administrator account to a minimum, as doing everyday stuff as an administrator is asking for trouble.

This user-level protection is what prevents one users processes intefering with another users, as they have different userid's so are kept seperate by the kernel. This means if one user accidentally downloads a malicious worm or virus, the damage is limited to just that users files and processes - not ideal, but better than letting it have full reign over the whole machine.

A big reason for the spread of malware in Windows OSs is that too many programs run as administrator, which can cause the whole system to be be affected if the program contains malware. If an OS *requires* the use of a virus checker, this is a sign that the OS isn't confident in its implementation of process protection. Virus scanners address the symptom, not the problem.

####Capabilities

Root access is a bit all-or-nothing, as it allows root all access to all resources. A refinement of the root idea is *capabilities*, which break access rights down into small parts e.g. right to access the network driver, access the filesystem, reboot the computer etc. This can be broken all the way down to rights to access individual files. These rights are called capabilities, and are like tokens that can be passed around and inherited by processes.

They allow finer control of security at the cost of a more complicated checking system. A few OSs, notable Flex, were built around the notion of capabilities and required hardware support to make things work with an acceptable speed - however, these never really took off. The idea has come back to modern OSs however. When Android installs an application, it asks the user whether that application should be allowed to access various system resources e.g. WiFi network access, phone contact list access, initiate phone calls etc.

Android calls these permissions rather than capabilities. It means that when an application runs, it can only access the resources the user has approved. This mechanism would be great if the user could be trusted to read and understand the list of requests.

####Inter-Process Communication

Many processes can be created, process then exit without needing to refer to any other process, but there are many processes that need to send data to, or receive data from other running processes. For example, a new program starting might wish to tell the process managing the display that it wishes to pop up a window on the display. Or, one process may have to wait for another process to finish some action (e.g. pop up a window) before it can progress itself - this is called *synchronisation*.

IPC can be acheived in many ways, but it must be supported by the OS, because by default the kernel tries to stop on process interfering with others. IPC contradicts this non-interference, so there must be rules and restrictions, or else onpe process could just blast another process with data, preventing it from doing any useful work.

######Files

The simplest way for two process to communicate is using an existing resource, namely files. Process A wishes to send some data to process B, so A writes it to a file and B reads it from the file.

There are issues however - which file to use? A and B need to agree on a filename to use. They can use a single "well known" file, but this is problematic if many processes are all writing to the same file simultaneously. They could have a seperate file for each pair of processes, but to agree on a file name A and B must have previously communicated.

Also, how can B know when data has arrived? It might have to repeatedly poll the file until the data arrives, which doesn't scale well to large numbers of files or processes. The file protections must also be set properly (with userids) to allow only the authorised processes to read and write to them.

Files are quite slow relative to other IPC mechanisms, and in general aren't used for IPC. However, they should be considered as a choice when *huge* amounts of data need to be transferred.

######Pipes

A pipe connects two processes together, taking output from one and feeding it as input to the other.  They have a fixed size: 4096 bytes is common. A writes to the pipe and B reads from the pipe independently of eachother, like with files. Bytes are read out in the same order they were written in (FIFO). Unlike files, pipes also provide elements of coordination and synchronisation.

If A tries writing to the pipe when it is full, or B tries reading from the pipe while it is empty, the process is blocked by the OS until space has been freed up by B reading some or until bytes are available by A writing some. Thus the scheduling of A and B will be affected.
