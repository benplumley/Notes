###Filesystems

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
