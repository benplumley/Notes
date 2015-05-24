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

While SSL/TLS is widely used and beleived to be reasonably secure if implemented correctly, it is under continual review as new attacks are discovered. The are mostly holes in implementations (Heartbleed, FREAK), but accasionally are holes in the actual protocol (CRIME).

A library layers over TCP, and gives a new transport layer that can be used very much like TCP. There are several decent implementations including OpsnSSL, GNUTLS, NSS and several others. Many protocols can layer over SSL/TLS instead of TCP to give a secure version. For example:
- HTTP, the protocol used to fetch pages, has a secure version layered over SSL/TLS called HTTPS.
- SMPTS, the protocol used to send email, has a secure version called SSL/TLS called SMTPS.
- IMAP, the protocol used to read amil, has a secure version called IMAPS.

There are overheads in using SSL/TLS:
- A one-off overhead of writing the application code to use SSL/TLS rather than TCP.
- A per-connection overhead of setup messages and the associated computation for checking certificates.
- A per-packet overhead of data expansion in the encoding of the encrypted data.
- A per-packet overhead of the computation required to encrypt and decrypt the data.

Big providers such as Google started to move their services to SSL/TLS, e.g. Google now uses HTTPS rather than HTTP to protect all of Gmail. For such a large company there is a significant cost in doing so, but the security gained makes it worthwhile.

SSL/TLS can also be used to provide a link layer, in the sense that you can use it to support a network layer. An example of this is OpenVPN, a virtual private network system. It uses SSL/TLS to create a link layer, and creates a new virtual network interface that the OS can pass IP packets to. 

The code behind this interface handles authentication, encryption etc. before handing the result on to a 'real' transport layer, usually UDP. The encapsulated data then goes down through the normal transport and netowrk layers and is transmitted over the real link and physical layers. At the receiving end, the real transport layer hands the data to OpenVPN, which decrypts and passes the resulting IP packets to the OS to pass up the rest of the stack via its virtual interface.

This allows applications to use encrypted private network, layered over an insecure public network. The big benefit here is that an unaltered application gets the security and authentication for 'free', and all applications are now secured at no effort to them. Additionally, the VPNs can tunnel IP packets across the public Internet to a secure destination network, such as your home network. This makes it appear that your computer is directly connected to, for example, your workplace network, wherever you happen to be plugged in. This is very useful for mobile workers to get easy access to work resources.

So a VPN creates a single, secure point-to-point connection that can be used by any unaltered application on the host. TLS on the other hand is coded into an application, which can then make a secure connection to any other host that runs TLS.
