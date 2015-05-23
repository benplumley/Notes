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

####IP

The network layer in the Internet Protocol is called IP. Its main function is to deal with the routing of packets. The packet header added by the IP has a hardware-independent network layer address, or an IP address. These are in the same format throughout the whole Internet:  
![](http://i.gyazo.com/fbccab14731dc794cc0202e1e564b67b.png)  

Source and destination IP addresses are four bytes long, typically written as four decimals. There is a structure in the IP address to help with routing: the first bytes (how many can vary) is the network address, identifying a network such as the University of Bath, and the last bytes are the host address, identifying a single host in the network.

This means that all packets destined for one network can be routed in the same way. Only when those packets enter the destination network is local knowledge needed. The host part is further split into *subnet* to help local routing within the university.

These addresses are independent of hardware, so they are the same on Ethernet as on WiFi or any other kind of network.
