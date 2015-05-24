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
