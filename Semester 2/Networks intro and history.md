###Networks History

The "Internet" (capital I) is the world-wide collection of networks. An "internet" (lowercase i) is an abbreviaton of "internetwork", which is just some collection of networks. An "intranet" is some collection of networks belonging to a single organisation. *The Web is not the Internet*.

The internet started as a project by the American Advanced Research Projects Agency (ARPA) in response to the Russians launching Sputnik (the first sattelite) during the Cold War. The idea was to connect the Agency's expensive resources, namely their computers, allowing them to be shared. The design was to be non-centralised to avaoid single points of failure, particularly nuclear attacks, so it was designed to have multiple paths between hosts.

Using simple circuits between machines would be too vulnerable, so *packet switching* was invented. Data is chopped into small chunks (i.e. packets), and each packet is sent individually, possible over different paths. The original data is then reconstructed at the receiving host.

This causes a few problems though. How is the data split? How are the routes found? How do we reconstruct the data from the packets? A packet doesn't know how to get to it's destination, and neither does the source host (unless it's on a local network). A packet is like a postcard with the address written on it, it relies on the *routers* it passes through to make the right decision.

To ensure maximum interoperability, the internet relies on standards and defined protocols. The use of standards means that two machines will be able to communicate with eachother, even if they are made my completely different companies, are of completely different techonologies, and have never previously interacted.

###Layering Models

To make two computers communicate, we need some hardware to cnnect them, so there must be some kind of electrical (or other) thing between them. They must then be compatible on voltages, how bits are represented as electrical or optical signals etc., and must agree on how to represent data as bits, e.g. signed or unsigned integers.

To implement a network system, we need to follow a sensible structured standard. Designing a standard like this is too big a problem to tackle all at once, so the design is split into layers, each with a well-defined functionality. A *layering model* for a system is a suggestion on how to split up the design - it is *not* a networking standard, but a recommendation on how to approach the design of the standard. After you have the standard, you can then make implementations based on the protocols the standard provides. To summarise:
- We pick a layering model
- We use this to guide us in making a standard
- The standard will specify various protocols
- Implementations will then follow and excute the protocols

It is very important that the protocols are documented clearly, so that implementations can follow them precisely without ambiguity or omission. Protocols include the expected interactions and interchanges between the entities (hosts) concerned, the messages involved, the message formats used, the actions expected of the entities etc., all so that the entities can agree on something. For networking purposes, this is that some data has been safely passed from one entity to another.

There are two main layering models in use for networks, the *ISO Open Systems Interconnection (OSI) Seven-Layer Model*, and the *Internet Four-Layer Model*. The OSI model is widely used in courses on networks, while the Internet model more closely resembles how things are done in the real world.

Layers should be:
- Easy to implement
- Represent a well-understood concept or abstraction
- Must only interface with its neighbour layers
- Chosen so that the meta-information flowing across boundaries is minimised

A layer must be as self-contained as possible and disregard all other layers as far as is possible, i.e. *modularity*. With modularity, an implementation of a layer can be removed and replaced without affecting the overall system.

There are 7 layers to the OSI model:

1 - **Physical layer**. This is the hardware layer, and deals with the transmission of bits over a channel. It handles things like what voltages/colours of light pulses/radio wavelengths to use, what encoding for bits, how long (in time) a bit should be, how many wires to use in a cable, what plugs to use on the cable... and much more. Generally, anything to do with choices regarding hardware.

2 - **Data link layer** (also called the *media access layer*, or MAC). This takes the physical layer and tries to create a channel where there are no undetected errors of transmission - we know that networks are not 100% reliable, so we must take into account the possible errors and deal with them.

A typical MAC layer sends the data as a sequence of frames, which are chunks of bytes, maybe tens of thousands of bytes long. If a frame is corrupted, the MAC layer may resend it, or maybe there is enough redundancy in the bit encodings to fix the error. Some link layers do this, while others just do nothing at all, letting higher layers figure out whats gone wrong and find a solution.

3 - **Network layer**. This layer controls the operation of the network, particularly the issue of *routing* data from source to destination. It can also deal with *congestion* - when there is too much data for a particular link, it might route some data via another link, or use *flow control* to slow down the rate of transmission. Alternatively if things are going well, flow control is used to speed up the rate of transmission.

4 - **Transport layer**. This accepts data from the session layer, and arranges it into packets suitable for the network layer, i.e. *packetisation*. In the other direction, it takes packets from the network layer and reassembles it into the original data stream, i.e. *depacketisation*. This will need to deal with packets arriving in a different order than they were sent.

5 - **Session layer**. This layer manages sessions between source and destination, for example a remote login session. Sessions can be quite short, e.g. just long enough for an email or web page to be transmitted, or arbritarily long. In general, a session is just some logically cconnected set of exchanges that have some unified identity, e.g. if the network crashes and reboots halfway through a big data transfer, the session can be picked up from where it left off, rather than starting again.

6 - **Presentation layer** - This provides a few things so that we don't have to reimplement them in every application. In particular, it decides on representations of data, such as characters, integers and floating point values. This means the source and destination can agree on how a particular stream of bits should be interpreted. So if the source wants to send the number 7, the presentation layer deals with encoding this in a suitable way, e.g. as some particular bits, and allows the destination to realise that this particular sequence of bits represents the number 7.

7 - **Application layer** - This is the only layer that most programmers see. It contains protocols like HTTP for the Web, SMTP for email, and so on. Built on top of these protocols are the applications that the users see, e.g. Firefox for the Web or Pine for email.

Remember - **People Don't Need To See Pink Alligators**. Sort it out, people.

Conceptually, data from an application is passed down through the layers until it reaches the hardware. As it passes from layer to layer it is *encapsulated* - a transformation of the data in such a way the the layer below can cope with it transparently, and in a way that it can be untransformed back again. At each layer, the transformation might:
- Add an identifying header or trailer (or both) that is needed for the functionality of the layer
- Encode certain bit patterns that might be misinterpreted or mis-transmitted by the next layer
- Put items in a standard form e.g. integers into a well-known format
- Do some arbritarily complicated manipulation
- Do nothing

Here is a diagram showing a possible (but unlikely) OSI encapsulation.
![](http://i.gyazo.com/29f915a67e32e2068dbc75adb83a368e.png)
