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

The machines storing the tables of nodes are called *name servers*, and their main purpose is to run DNS. Every host knows the IP address of one or more nearby nameservers, either in a file or through DHCP. When a host needs an address from a name, it sends a request containing the name to one of these local servers. If the destination name is in the same network as the requesting host, the table will have an entry for that destination.

For instance, to request moodle from LCPU:
- The host at lcpu.bath.ac.uk sends a DNS request containing 'moodle.bath.ac.uk' to adns0.bath.ac.uk
- adns0 sees that moodle.bath.ac.uk is in the network it manages, bath.ac.uk
- adns0 looks moodle up in its table of names and addresses
- adns0 sends this address back to lcpu

However, if the destination was not in the local network, a *recursive lookup* must be performed. The DNS server sends a *Start of Authority* (SOA) request to a random top level server to find out who is responsible for the top level label. This top level server responds with the relevant DNS server's name and address.

For instance, to request news.bbc.co.uk from LCPU:
- The host at lcpu.bath.ac.uk sends a DNS request containing 'news.bbc.co.uk' to adns0.bath.ac.uk
- adns0 sees that this address isn't in its local network
- adns0 sends an SOA request to a.root-servers.net for the 'uk' label
- a.root-servers.net replies with 'ns1.nic.uk' and its IP
- adns0 sends an SOA request to ns1.nic.uk for the 'co.uk' label
- ns1 replies with 'ns1.nic.uk' and its IP address (coincidentally, because this server manages both uk and co.uk)
- adns0 sends an SOA request to ns1.nic.uk for the 'bbc.co.uk' label
- ns1 replies with 'ns.bbc.co.uk' and its IP address
- adns0 sends an *address* (A) request containing 'news.bbc.co.uk' to ns.bbc.co.uk
- ns responds with the IP address for news.bbc.co.uk
- adns0 sends this back to lcpu
LCPU now knows the IP address of news.bbc.co.uk and can request a webpage from it. The whole system looks like  
![](http://i.gyazo.com/e9869f60817908c34c1a2e72ff186694.png)  

These responses are cached by the local server so it doesn't have to do a lookup every time. This is true of each label in the address - a request for www.bbc.co.uk will match the local server's cache entry for bbc.co.uk, so it can send the A request straight to ns.bbc.co.uk without the rest of the lookup. Because IP addresses can change, each cache entry has a time to live.

The benefit of using a local DNS server is that so many items will be cached. Someone else in the network having looked up the same destination, or even one with one or two matching labels, will drastically cut lookup time and network traffic.

The global network of DNS servers can also perform a *reverse lookup* - that is, find a domain name given an address. This is done by sending a request for the IP address with its octets reversed, prepended to .in-addr.arpa. The recursive lookup will be performed, and eventually, rather than A request, a pointer (PTR) request will be sent, returning a name.

DNS is very successful, and scales easily to all accomodate the number of hosts on the internet. Lookup takes milliseconds, which is helped by caching, particularly of intermediate results.

The relationship between names and addresses is actually many-to-many. More than one name can resolve to the same IP address. One of these names will be the *canonical name* (CNAME) and any other will be an *alias*. Similarly, one name can resolve to different addresses each time it is resolved. This allows the load to be shared between many servers, potentially preferring geographically closer ones.
