Databases not only store data, but also provide functionality through stored procedures. They also act like servers in that clients which access them can run on any platform and be written in any language.

There are risks with using databases, however.
- Crackers can sabotage the data or steal it. This can be prevented with backups, honest staff, secure and up-to-date software, logging and testing.
- The database or any part of the stack can fail. This can be prevented by using a reliable stack and having redundancy in components and systems.
- The laws regarding data storage can change. This can be dealt with by monitoring legislation and joining associations.
- The company can outgrow its data storage systems. This can be prevented by proper handling of concurrent requests and easily scalable design.

If confidential data is exposed, the company will face fines and lose customer trust. Data such as medical records, payment details and passwords should be stored on a server that isn't completely web-accessible. Users should be required to authenticate themselves with a properly encrypted password, and only able to connect over a secure connection. The database server should be in a physically secure location.

Data modification can be hard to detect if only small changes are made. This can be prevented with proper security and authentication, and monitoring of changes.

Denial of service attacks are hard to defend against, but their effects can be limited by redundant servers and specialised services.

Repudiation is where one party to a transaction denies having taken part. This can be preveted with the use of password-based authentication and digital certification.

Software errors can also pose a threat, if the software specification was wrong, the developers made false assumptions or there was inadequate testing. This can be prevented with user involvement in development and contingency plans.

The types of data storage are volatile storage, non-volatile storage and stable storage. Data is stored in a hierarchy of how often it will need to be accessed.

*Volatile* storage needs power to retain its data. If power is cut, the data is lost. Memory is volatile storage. In the hierarchy, this is primary storage.

*Non-volatile* storage can survive power outages, but is slower to access. Magnetic disks are non-volatile storage. This is secondary storage or *online storage*. Other non-volatile storage media, such as magnetic tapes and optical storage, are *tertiary storage* or *offline storage*. These have the slowest access times.

*Stable* storage is a theoretical medium that survives all failures. It can be approximated using multiple copies of the data in different locations on different non-volatile storage media.

The storage hierarchy  
![](http://i.gyazo.com/6be7f6584cefa18b88fc70b2201b38a3.png)

Magnetic disks are the primary medium for long-term storage of data. They are slower to access than memory, but are cheaper and non-volatile. The data on them can still be destroyed by disk failure, but this is relatively rare. Data is recorded by polarising magnetic cells on a spinning platter to face in one of two directions using a read-write head.
