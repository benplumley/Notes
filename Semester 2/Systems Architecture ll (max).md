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
