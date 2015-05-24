###SSL/TLS

The protocols *secure sockets layer* (SSL) and it's more modern variant *transport layer security* (TLS) provide secure communications over the Internet. The internet was designed in a safe academic environment with little thought given to privacy, so even today most data on the Internet is readably by all intermediate routers as it passes from source to destination.

SSL/TLS layers on top of the transport layer, particularly TCP, and provides privacy and authenticaton. It also prevents:
- Tampering, e.g. changing the message "send Jim £10" to "send Bob £50".
- Forgery, e.g. creating a message that appears to come from a bank.
- Replay, e.g. re-sending a message (your own or someone else's).

The need for secrecy is well-understood, but authentication less so, and is arguably more important. You could have a military-grade secure connection to some trustworthy website, so you enter your card details knowing that noone else can read them, only to learn that the Web page was a scam, and not the page you thought it was. This is an example of how knowing who you are talking with can be more important than keeping what you say a secret.

Although SSL/TLS lives on top of the transport layer, it is often used *as* a transport layer by applications. This works because of layering - the layers above are unaffected and use SSL/TLS just like any other transport layer, so there is minimal change needed to an application to get it to use secure communications.

TCP is managed by the OS kernel, but SSL/TLS is in user program space, meaning the application programmer has to invoke it when needed. This gives the programmer full control over the security and authentication of their program. If an application wants security or authentication, the programmer simply does an SSL/TLS setup on top of a normal TCP or UDP connection, and then reads and writes from the SSL/TLS connection.

Once authentication is acheived, the endpoints can negotiate a secure and private connection. The authentication mechanisms are quite complex, but essentially use mathematics to mimic real-world authentication mechanisms e.g. documents or certificates that prove identity e.g. passports, or prove a property e.g. driving licence.

SSL/TLs allows authentication in both direction, meaning the server can authenticate the client and the client can authenticate the server. For example, a bank can be sure it is talking to a real customer, and the customer can be sure they are talking to the real bank. Each is optional, but both are recommended.

However, banks typically use usernames and passwords to authenticate the user, not SSL/TLS, because this would involve the user generating and managing a certificate, and sending it to the bank by some seperate, authenticated mechanism. This would be too hard for most users, and would cost the bank a lot in certificate management, so usernames and passwords are used instead.

Example: If a Web browser wishes to authenticate a server, it sends to the server a request for a certificate using SSL/TLS. The Web browser already contains a collection of certificates from certification authorities - companies that sell certification services. The browser can use these to verify that the certificate returned from the server is real. Clever maths is used to prevent forgery of these certificates.
