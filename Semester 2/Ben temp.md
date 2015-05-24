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
