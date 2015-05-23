####IP

The network layer in the Internet Protocol is called IP. Its main function is to deal with the routing of packets. The packet header added by the IP has a hardware-independent network layer address, or an IP address. These are in the same format throughout the whole Internet:  
![](http://i.gyazo.com/fbccab14731dc794cc0202e1e564b67b.png)  

Source and destination IP addresses are four bytes long, typically written as four decimals. There is a structure in the IP address to help with routing: the first bytes (how many can vary) is the network address, identifying a network such as the University of Bath, and the last bytes are the host address, identifying a single host in the network.

This means that all packets destined for one network can be routed in the same way. Only when those packets enter the destination network is local knowledge needed. The host part is further split into *subnet* to help local routing within the university.

These addresses are independent of hardware, so they are the same on Ethernet as on WiFi or any other kind of network.
