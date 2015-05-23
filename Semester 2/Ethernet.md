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
