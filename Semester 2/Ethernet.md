####IP

The network layer in the Internet Protocol is called IP. Its main function is to deal with the routing of packets. The packet header added by the IP has a hardware-independent network layer address, or an IP address. These are in the same format throughout the whole Internet:  
![](http://i.gyazo.com/fbccab14731dc794cc0202e1e564b67b.png)  

Source and destination IP addresses are four bytes long, typically written as four decimals. There is a structure in the IP address to help with routing: the first bytes (how many can vary) is the network address, identifying a network such as the University of Bath, and the last bytes are the host address, identifying a single host in the network.

This means that all packets destined for one network can be routed in the same way. Only when those packets enter the destination network is local knowledge needed. The host part is further split into *subnet* to help local routing within the university.

These addresses are independent of hardware, so they are the same on Ethernet as on WiFi or any other kind of network.

The problem now is that to send a packet, we need to know both the hardware address and the software address. Given a host's IP address, we need to find the corresponding Ethernet address. This is done by the *Address Resolution Protocol* (ARP). This is a protocol in the link-layer that broadcasts an ARP frame on the local network asking who has that IP address. The host with that IP address responds with its Ethernet address. These values are cached by each host, and expire in case a new machine takes that IP address.

This works when the host and destination are on the same network. If they aren't, the packet is instead sent to the gateway host and the process of non-local routing begins. In this case, the hardware address would be of the gateway and the software address would be of the destination host, two different machines.

The reason both hardware and software addresses are needed is because with non-local routing they refer to diferent things: the hardware address is for the next hop and the software address is for the ultimate destination. ARP isn't specifically for IP and Ethernet, it can pair and physical (hardware) and network layer (software) addresses.

####DHCP

When a machine is set up or turned on, it doesn't have an IP address. It uses the *Dynamic Host Configuration Protocol* (DHCP) to get one. When the machine is newly connected to a network, it makes a DHCP broadcast to the network, to which a special-purpose DHCP host must respond. This machine will read the request, choose an unused IP address, and send it back to the requesting host. The new host configures itself to use this address.

When a host is turned off, it is supposed to inform the server via DHCP that it is finished with the address so that it can be added back into the pool of free addresses. However, some hosts ignore this and sometimes it's impossible (eg in a powercut). This is solved by giving each address a lease time, after which the address expires.

If this expires while it's being used, the host can renegotiate use of the same address through DHCP. Lease times depend on the situation - for instance, in a coffee shop, hosts might only connect for tens of minutes, so this is a suitable lease time. In a data centre, the same hosts will likely be connected for months at a time, meaning long leases with little overhead can be used.

DHCP also supplies to new hosts the address of the gateway, the addresses of name servers (DNS), lease times, and the addresses of servers for things like printing and mail.

####IP Addresses

The problem with 4-byte IP addresses is that there aren't enough of them for all the computers - 2^32 is around 4.3 billion addresses, clearly not enough for a population of 7 billion. This 4-byte system is called IPv4, and is slowly being replaced by IPv6.

IPv6 replaces the network layer protocol with a new protocol using 16 byte addresses. This should have been a drop-in replacement, with the link and transport layers being unaffected, but mistakes made when designing TCP and networking APIs mean that mainstream use of IPv6 will probably not happen for a long time.

IPv4 and IPv6 do not interoperate, however they can both run side-by-side on the same physical layer. This will be the case until IPv4 is completely replaced, which might take a very long time.

####DNS

As well as hardware and software addresses, machines have human-readable names, such as lcpu.bath.ac.uk. This makes the internet easier to use because we don't have to remember IP addresses (which can change anyway). In the early Internet, each machine had its own lookup table of names and addresses. As the Internet grew, this stopped being feasible. A protocol called *Domain Name System* (DNS) is used instead.

DNS servers now perform the job previously performed by each host, storing a table, keeping it up-to-date, and looking up addresses from names. These are distributed throughout the Internet for speed and security.

Names are heirarchical: lcpu.bath.ac.uk refers to a machine called lcpu in the domain bath.ac.uk (Bath University), which is in the domain ac.uk (JANET), which is in the domain uk. This is in the root domain. Each node in this tree is called a label.

This tree is also used to distribute the database. The root node, '.', is managed by ICANN. This means they control the *top-level domains* (TLDs) such as com and uk. They keep the lookup tables for the root level say who can get labels in the next level, and charge those people money to do so. They delegate the management of lower labels to other organisations.

- Labels under the root node are managed by ICANN.
- Labels under uk are managed by the Network Information Centre (NIC).
- Labels under ac.uk are managed by the United Kingdom Education and Research Networking Association (UKERNA).
- Labels under bath.ac.uk are managed by the University of Bath.
- Labels under cs.bath.ac.uk are managed by the Computer Science department.
