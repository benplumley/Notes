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
