####Inodes

An inode is a fixed size structure stored on the disk, that contains the metadata of a file (all the information about it). The traditional Unix filesystem is based on inodes, and each file is described by one. Information in the inode includes:
- Timestamps - Dates and times this file was last accessed and last modified.
- Ownership - The userid of the owner of this file, for protection purposes.
- Size
- Type - Whether this is a plain file, a directory, or some other kind of special file.
- Access permissions - Who can read or write or run this file, if it is a program.
- Reference count - The number of names this file has.
- A list of the areas on the disk where the actual data lives.
