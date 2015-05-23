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

1 - **The physical layer**. This is the hardware layer, and deals with the transmission of bits over a channel. It handles things like what voltages/colours of light pulses/radio wavelengths to use, what encoding for bits, how long (in time) a bit should be, how many wires to use in a cable, what plugs to use on the cable... and much more. Generally, anything to do with choices regarding hardware.

2 - **The data link layer** (also called the *media access layer*, or MAC).

