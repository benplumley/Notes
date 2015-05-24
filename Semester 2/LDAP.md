###LDAP

LDAP stands for *lightweight directory access protocol*. While DNS is a directory of names and addresses aimed at the network layer, LDAP is a more general directory aimed at the application layer.

The difference between database and directory is that a database is a big collection of data optimised for concurrent reads and updates, while a directory is a big collection of data optimised for mostly reading, with the occasional update.

LDAP is used to store anything you like, often things like usernames, passwords, email addresses etc. It shares many properties with DNS:
- It is distributable - Items of data can be on remote machines.
- It can be replicated - For resilience and speed.
- It is hierarchical - But keys can be more complicated than simple DNS labels.

Unlike DNS, that data stored by LDAP can be arbritary chunks of data (numbers, pictures, sounds etc.), not just IP addresses. Also, lookup can use complicated filters, e.g. "find all people who's names start with W and date of birth is before 200", if suitable expressed in the LDAP language.

A popular use for LDAP is to store passwords for large networks. When you have a network of computers where any user can sit down and use any of the computers, determining who is a valid user becomes a problem. Rather than having a complete list of all authorised users and their passwords on all machines (as used to happen), we instead use an LDAP server. This is a host (or more than one, for resilience) that has the password in an LDAP directory.

When a user logs into a machine, that machine refers to the LDAP server for authentication. Administration (e.g. changing the password) is very easy - just update the LDAP server. Microsoft's Active Directory and NDS, Novell's directory service, both build on LDAP.

LDAP is widely used, but mostly invisible. We could use LDAP in place of DNS, but LDAP is a more general mechanism and so would be slower, and the management of LDAP servers is somewhat more fiddly.
