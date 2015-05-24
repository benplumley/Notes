####Services

A service is just where a client makes a request and the server fulfills that request. DNS is a service, as are LDAP and other databases, remote disk access, and the web. This can be extended to arbitary computations.

One such example is *remote procedure call* (RPC). We can put a function onto another machine and, rather than just requesting data from that machine, request it to perform that function and return the result to the client. This could be for several reasons
- the function is computationally expensive so it makes sense to offload it
- the data needed are stored on the remote machine
- the data needed are not available to the public
- the program to calculate the result is not available to us  
![](http://i.gyazo.com/6a49b4d62907eaade9c7a28d15de0c7a.png)

RPC is quite a simple mechanism, but only useful in cases where the reasons hold. Otherwise, it introduces unnecessary network latency into code that would be faster locally.

*Web services* use the idea that fetching a webpage isn't very different from RPC. We can encode our data using a protocol such as SOAP or JSON and send it to the server over HTTP.

Web services also allow service discovery through the *web services description language* (WSDL). This language allows us to describe what service we want performed. The *universal description discovery and integration* (UDDI) protocol published and allows discovery of services through servers acting as service brokers, whose purpose is to support discovery.
- A server uses WSDL to register with a service broker
- A client wishes to compute a function
- It asks the broker for a suitable server using WSDL
- The broker replies
- The client sends its request to the server
- The server computes the result
- The server replies

SOAP is an extension of XML. It is very verbose and therefore slow to transmit, generate and parse.

Web services are very popular, especially between businesses. They are system independent and standardised so anyone can register with a broker and interoperate. Examples include IBM WebSphere and Globus Toolkit. As these services run using HTTP, they can also easily run on HTTPS and be secure.
