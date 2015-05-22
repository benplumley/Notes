####Inodes

An inode is a fixed size structure stored on the disk, that contains the metadata of a file (all the information about it). The traditional Unix filesystem is based on inodes, and each file is described by one. Information in the inode includes:
- Timestamps - Dates and times this file was last accessed and last modified.
- Ownership - The userid of the owner of this file, for protection purposes.
-
