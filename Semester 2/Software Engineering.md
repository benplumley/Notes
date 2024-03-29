#CM10193 - Software Engineering
##Dr Leon Watts and Dr Fabio Nemetz

###Software Systems

A **system** is a purposeful composition of parts, i.e. multiple components working together as a single entity, e.g. a car as a collection of moving mechanical components, or an animal as a set of living biological parts.

System properties:
- Robustness, maintainability, usability
- Result from component relationships e.g dependencies between code modules.
- Dynamic performance of overall system

**Subsystems** are components of larger systems that *can* operate independently, but *don't* operate independently when incorporated into larger systems, e.g. a GPS in a car navigation system.

A **Software System** is a set of software components in technical and social environments. Components 'take charge' of sets of operations and responsibilities and interact through interfaces. Properties of a good software system include:
- Actually delivering the required function
- Usable - must make sense to the user it was defined for and fit with the demands of their work
- Maintainable - must evolve to meet changing needs
- Dependable - must be trustworthy
- Efficient - should not be wasteful of system resources

The complex relationships between the components in a system mean that a system is more than simply the sum of its parts. It has properties that are properties of the system as a whole and cannot be attributed to any specific part of the system, known as **emergent properties**.

Some key challenges faced in software engineering are:
- **Heterogeneity Challenge** - Building dependable software to cope with the heterogeneity (diversity) of existing computer systems, support structures, and legacy software.
- **Delivery Challenge** - Shortening delivery times for complex systems without compromising on quality.
- **Trust Challenge** - To develop techniques that demonstrate software can be trusted by its users.

**Technical computer-based systems** include both hardware and software. The operators and operational processes are not normally considered to be part of the system. They are not self-aware.

**Socio-technical systems** *include* technical systems, as well as the operational proccesses and the people who use and interact with the technical system. They are non-deterministic, and governed by organisational policy.

**Project Scheduling** involves estimating the time and resources required to complete activites and organise them into a coherent sequence. The project should be broken down into distinct tasks, with an estimated duration. Contingencies should be allowed for.

A **Gantt Chart** is used to represent the structure of the team's work, showing the tasks the project has been broken down into over time. It is designed to allow planning and monitoring of tasks. It gives a clear impression of task timing, clearly showing what needs to be done and when and any concurrencies. However, it is not so effective in showing dependencies and personnel responsibilities.

A Gantt Chart:
![](http://i.gyazo.com/a09a559ee3f3f56df6ae65bd38e39718.png)

###Ethics and Professional Conduct

**Codes of conduct** are set by professional bodies or institutions, and are necessary to maintain professionalism. They are typically a set of principles that are meant to guide rather than prescribe. Therefore they are often ambiguous in application and must be used in aid to professional judgement in ethical dilemmas.

An example of ethics in the real world is the US Challenger space shuttle disaster in 1986. There were problems with the O-rings in relation to cold launch conditions, which was noted by an engineer. However, no testing was done due to more pressing problems. The engineers unanimously recommended against the launch, however Space Centre was "surprised and appalled" at the recommendation, and went ahead with the launch due to political and financial pressures. The O-rings failed and the shuttle exploded 73 seconds into the mission, killing all seven crew.

There are 8 main principles in the **ACM/IEEE Code of Ethics**. These are:

1. Public - Software engineers shall act consistently with the public interest.
2. Client and Employer - Act in the best interests of their client and employer, consistent with the public interest.
3. Product - Products and related modifications shall meet the highest professional standards possible.
4. Judgement - Integrity and independence in their professional judgement.
5. Management - Adopt and promote an ethical approach to the management of software development and maintenance.
6. Profession - Advance the integrity and reputation of the profession, consistent with the public interest.
7. Colleagues - Be fair and supportive of other colleagues.
8. Self - Software engineers shall adopt both a "lifelong learning" and ethical approach to the practice of their profession.

There are many potential difficulties with codes of conduct. They can be ambiguous, parts of it may conflict, and you may find yourself in situations which are not covered by the code, in which case you are expected to behave professionally and use your best judgement. Codes of conduct are also subject to continual development.

The **B.C.S. Code of Conduct** (revised 2011) is as follows:

1. **Public Interest**. This takes into account public health, privacy, security and well-being of others and the environment. It also covers legitimate rights of third parties, and discrimination on grounds of sex, sexual orientation, maital status, nationality, colour, race, ethnic origin, religion, age or disability.
2. **Professional Competence and Integrity**. Do not claim to be competent when you know you are not. Develop your professional knowledge and skills (lifelong learning). Respect and value alternative viewpoints. Reject bribery.
3. **Duty to relevant authority**. Respect confidentiality of information unless the law requires disclosure. Avoid conflict of interest between work and relevant authorities.
4. **Duty to Profession** Uphold the reputation of the profession. Encourage and support fellow members in thier professional development.

The **UK Computer Misuse Act** supports prosecution of computer related crime. A person is guilty of an offence if he/she causes a computer to perform any function with the intent to secure access to programs/information on any computer, and if that access is unauthorised (and he/she knows this at the time). Causing unauthorised modification of a computer material is a more serious offence. It doesn't matter where the access was made from, or whether the offender is a British citizen.

###Models of Software Engineering Processes

A **Software Processes** is an organisational mechanism for controlling software development. It has a 'lifecycle' that depends on its environment, and it ensures that software products meet the needs for which they were commissioned. They are a defined set of activities and associated results that produce a software product. There are several different models e.g. waterfall. Activities common to all software processes are:
- Software specification
- Software design and implementation
- Software 'validation'
- Software evolution

A **software process model** is an abstract representation of a process. It presents a description of a process from some particular perspective. It is a simplified version of reality, and is useful for planning and managing SE projects.

The **waterfall process model**:
![](http://www.cs.odu.edu/~cs333/website-latest/Lectures/waterfall/page/waterfall0.gif)

In the waterfall model, specification precedes development. One phase has to be complete and officially signed off by the client before moving onto the next phase (sign off means that the SE team won't go back and improve or redefine earlier work). This is suitable for projects that have 'change proof' requirements, e.g. large multi-site engineering projects, stable business environments. This creates a very clear project management model, with easy allocation of responsibility and milestones at the end of each activity. However it is difficult to respond to changing requirements - few business systems have stable requirements, and the clients operations may change too.

Another process model is **formal development**. A waterfall-like process is used, with a formal specification (uses logical notation). However it is refined through several transformations to a design that can be implemented.

**Iteration** is very important in process models. There is almost always pressure to change system requirements in the course of a project - This means results of earlier activities must be reworked, and implications for later activities must be considered. This produces unpredictable results unless managed. Iteration can be applied to any of the generic process models, but is hard to do effectively. However, some special process models have been invented to systematically handle iteration.

**Incremental software processess** have development and delivery broken down into increments, where each increment delivers useful service. Requirements are *well defined and prioritised*. High priority requirements are frozen and included in earlier increments. Requirements for later increments can continue to be defined whilst earlier increments are constructed. This model means that users gain immediate value, as the highest priority services are delivered first, so they don't have to wait as long for useful services. There is also a lower risk of project failure, because it is unlikely that no increments will be delivered, and high-priority services are completed first and therefore receive the most testing. Users can also gain experience from early increments as prototypes, improving requirements for later increments.

However, the incremental software process can lead to trust problems, as the clients don't know exactly what they are getting. Also there may be multiple dependencies in very large projects, which may make it too difficult to decouple system components and break the process down into increments.

Abstract model of an incremental software process:
![](http://i.gyazo.com/3e26e7c9f19be0c2ca9c3b08887f47e3.png)

**Agile methods** were developed to promote rapid and adaptable software development, and have become more and more common in recent years. They focus on the production of working software rather than design and documentation. The key principles of agile methods are:
- Customer involvement
- Incremental delivery
- People not process
- Embrace change
- Maintain simplicity

Abstract model of a generic agile cycle:
![](http://i.gyazo.com/1615d952744b384874a6d15c78ebda92.png)

An example of an agile software process model is **eXtreme programming (XP)**. The client is part of the development team, and new versions may be built several times a day. Requirements are simply 'story cards' developed from user scenarios, and the test-first approach to development reduces the chance of new increments introducing errors into the existing software. This uses scripts for automated testing. It also features pair programming on shared workstations, which leads to constant informal reviewing and promotes refactoring. However, this can be perceived as constraining and invasive, and it requires a small co-located team that are happy to do pair programming.

Abstract model of a generic cycle with the XP proccess model:
![](http://i.gyazo.com/87571ddedce23b445b7ccfbd26d41ff0.png)

The **spiral model** is a software process represented as a spiral, rather than a sequence of activities with backtracking. Each loop in the spiral represents a phase of the software process. Risk are explictly assessed and resolved throughout the process. There are no fixed processes e.g. specification or design, and loops in the spiral are chosen as required. There are four sectors of the spiral model:
- Objective setting - specific objectives for the phase are identified.
- Risk assessment and recution - risks are assessed and activities put in place to reduce key risks.
- Development and validation - a development model for the system is chosen which can be any of the generic models.
- Planning - the project is reviewed and the next phase of the spiral is planned.

Abstract model of a generic spiral model:
![](http://i.gyazo.com/87f8424666b35aa269a5e8dd08e878b3.png)

###Requirements - Gathering Evidence

Requirements can come from a variety of sources:
- Computer science literature (technical articles and case studies)
- Domain information (descriptions of work from company documents from trade or professional bodies)
- Information about commercial systems (vendor websites and reviews)
- Interviews with primary, secondary and tertiary users
- Observations of people who are currently in similar situations.

However, people often struggle to express what they need in terms a software engineer would understand. Alternatively, what they think or say they would like to have may not be what they would actually like to have. Also, people may want different things - stakeholders can only tell you about their own part of the problem, and may disagree with one another. New stakeholders may also become involved, and the business environment may change.

There is not a single solution to the problem of defining system requirements. **Viewpoints** represent the perspectives of different stakeholders and help to organise requirements information. They also identify integration challenges, keep track of conflicts and tensions and allow multi-perspective analysis. There are 3 different types of viewpoints:
- Interactor viewpoints (primary and secondary users) - People or other systems that interact directly with the system.
- Indirect viewpoints (tertiary users) - Stakeholders who will not use the software system themselves, but who influence ther requirements.
- Domain viewpoints (e.g. standards, rules) - Domain characteristics and constraints that influence the requirements.

In software engineering, an **interview** is a guided conversation between one or more engineers and one or more 'domain experts'. The SE team prepares questions to stakeholders about their current sociotechinical system, and the software system to be developed. They are *good* for getting an overall understanding of stakeholders viewpoints (what they do, how they might interact with the system), but *not good* for understanding domain requirements - requirements engineers cannot understand specific domain terminology, and some domain knowledge is so familiar that people find it hard to state or don't think it's worth explaining. Interviews can be *fully-structured*, in which interviewers stick to a set of pre-defined questions, or *unstructured/semi-structured*, which use prompts and guides but no rigid agenda, and explore a range of issues with the stakeholders.

Issues with interviews:
- Deciding which users to interview or observe, taking budget and schedule into account.
- Devising a scheme for bringing together data, with an indexed and secure archive for raw data and structured requirements statements linked to the data.
- Selecting equipment e.g. notebooks, pens and cameras (static information) or voice/video recorders and batteries (dynamic information).

For effective interview practice, there are many things to consider:
- You must introduce yourself - Say who you are, the purpose and duration of the interview, and the recording method to be used.
- Warm-up - make the first questions easy and non-threatening.
- Main body - present questions in a logical order.
- Closure - signal the end of the interview and thank the interviewee.
- Be open minded - be prepared to ask *and* listen, and avoid pre-conceived ideas about the software system to be constructed.
- Prompt the interviewee with questions or proposal - don't simply expect them to respond to questions like "what do you want". Ask what they do, and build on the things they say.

Ethical interview practice is also important. A written summary of the purposes of the interview should be prepared, including the goals of the interview, what will happen to the findings, and how their privacy will be safeguarded. Consent must be obtained from the interviewee, with a time and place arranged. They should also be informed that they will be asked before being quoted, that they can stop the interview whenever they wish, and that they have the right of correction.

###Functional and Non-Functional Requirements

Requirements define all aspects of a system engineering project; its capability and operational characteristics, the development process for creating the system etc. They are sets of structured and inter-related statements, with high-level features and low-level detail.

**Functional requirements** are statements of services, features or functions that the system should provide. They commonly relate inputs to outputs.

**Non-functional requirements** are general properties of the system and its behaviour. They are constraints on development and delivery. Examples of system properties are usability, performance and responsiveness, safety and security. Examples of constraints on development are process stipulations e.g. delivery schedule, quality assurance standards, and technologies to be used (infrastructure and legacy). Non-functional requirements should be structured as follows:
- Product requirements - Specifications about how the system must behave e.g. execution speed, system reliability, downtime limits.
- Organisational requirements - Compliance with organisational policies and procedures e.g. process standards used, implementation requirements.
- External requirements - Wider constraints on the system and its development process e.g. legal compliance, professional standards, interoperability requirements.

It is very important for the requirements to be clear and precise, otherwise the wrong job may get done. Developers could misinterpret the clients' needs, and team members may be working against each other if they interpret requirements differently. Also, dependencies between requirements may be missed, halting further work until the dependecy is completed. Some functionalities may be duplicated, and there may be conflicts in subsystem operations.

Imprecise requirements cannot be verified. For example, instead of "must be fast", use "number of transactions per second/hour/day" or "response time (milliseconds, seconds, minutes)".

Requirements statements should be formatted with an index number and concise name for the requirement ("5.3.6 Daily data recovery script"), a priority (high medium or low) and a statement ("The system should execute a test script at 21:00 hours each day to retrieve five files from the most recent backup"). It should also have an author/source, and any dependencies and relationships.

Changing a requirement can have a knock-on effect on any requirements that depend on it - to solve this, a method is needed to track which requirements depend on which others. An example of this is a square table with columns and rows as requirement numbers and a mark where the column depends on the row.

Good requirements, therefore, must be  
- Prioritised  
- Correct in that they are based on what the client needs, not what the developer wants to make  
- Modifiable, because they will need to be changed during the project  
- Traceable, so dependencies can be resolved easily  
- Unambiguous  
- Verifiable

These are known as the *six essential properties* of requirements statements.

###High-Level Models of Software and Architectural Design

Programming is a type of problem solving. Programming a system can be thought of as splitting the system down into smaller and smaller subsystems and tasks, until each individual task is small enough to be written in a single line of code.

An **architecture** describes how the system will be split up into manageable parts. These will probably correspond to the different parts of the problem the system is trying to solve. Software architecture, therefore, is a strategy for reducing complexity whilst adhering to functional, performance and cost goals. It requires the system to be separated into modular components, and describes their connection.

The benefits of architectural design are  
- It helps stakeholder communication because they can be shown a coherent model and provide feedback on it  
- It allows for large-scale reuse because the individual modules will work on their own or as part of a different system
- It supports thinking about non-functional requirements.

If each module corresponds to a group of dependent requirements, then any change in requirements will hopefully only affect that one module. Grouping dependent requirements into the same module means that changes can be implemented more quickly and with less potential for integration problems.

An architectural design document consists of graphical models and text explaining them. Architectural models can be static, showing the layout of the system, or dynamic, showing how it will run. An example of a static structural model is a box-line diagram.

The organisational style should be decided on early in the design process. It defines how the subsystems will communicate and be layed out.

A common organisational style is the **repository model**. Subsystems may only exchange information through a central repository. This is popular with systems that generate and consume a large amount of data. Benefits are  
- Backup, recovery and security of the data is centralised because the data is stored in one component  
- The producers of the data don't need any logic relating to how it is consumed, ie who to send it to  
- Sending data is efficient because it only needs to be sent once and then any subsystem that needs it can read it  
- It is easy to integrate new subsystems without changing the current ones

Some disadvantages are  
- A central repository is a single point of failure. If the repository fails, none of the subsystems can work  
- Subsystems must compromise in what they can do in order to conform to the data structure expected by the repository  
- It is very hard to change the format of the data expected by the repository because all of the subsystems depend on it being in a certain format  
- Different subsystems may want different backup or security policies but only one policy can be applied to all data. For instance, if one subsystem handles sensitive data and the others handle publicly available data, all of the data must be encrypted despite the computational overhead.

Another organisational style is the **client-server model**. Subsystems fit into one of  
- Server subsystems, which offer services to other subsystems  
- Network subsystems, which offer communication and notification between client and server  
- Client subsystems, which use the data and services provided by the servers. A thick client is   mostly independent of its servers; a thin client is highly dependent on the servers.

Clients access the servers by sending a request over the network subsystems and receiving a reply from the servers over them. The numbers and identities of clients don't need to be known about by the servers, and the clients only need to know about the servers relevant to them.

Advantages are  
- Servers and clients can be upgraded without impacting the operation of the system
- There is no shared data model, so each subsystem can handle its data in the most appropriate way for that data

The main disadvantage is that clients are not guaranteed to be able to take advantage of server upgrades, and may have to be upgraded themselves.

When choosing an organisational structure and designing the system architecture, five factors must be considered: performance, security, safety, availability and maintainability.

Performance is improved by localising critical operations within a small number of subsystems, and having minimal communication between these subsystems.

Availability is improved by building components in such a way that a broken component can be swapped out for a redundant version without bringing the whole system down. This is called hot-swapping.

Safety is improved by putting all safety-critical operations in a single subsystem, or as few as possible. This reduces the complexity of the safety validation, making it easier to be sure that the safety measures implemented work properly.

Security is improved by using a layered model, where the most critical information is stored in the innermost layers and each layer can only communicate with its immediate neighbours. This allows security validation to be implemented more easily.

Maintainability is improved by using fine-grained components which can easily be substituted for alternatives. This reduces code coupling. Shared data structures, such as in a repository model, should be avoided to improve maintainability.

###Context and Scope

The requirements document will have two groups of users. The client organisation will have users, such as business managers, end users and the administrators who will support and maintain the system. The developer organisation will have users such as the architects, developers, managers and testers.

Software systems exist in a context, which is the environment the system will fit into. They are usually themselves subsystems of a larger business or organisational context.

The architects must scope the system to decide which parts of the client's problem is to be solved by the system. They must also decide how much of the problem context is relevant to the development. Scoping the system requires the architects to set boundaries on the intended features of the system. They must decide which functions will be handled by the software and which goals the software must meet.

The IEEE has a standard defining how a requirements document should be layed out. The standard for a *Software Requirements Specification* consists of  
- Section 1 Introduction  
- Section 2 Overall description  
- Section 3 Specific requirements  
- Appendices  
- Index  

The descriptions of each requirement are in English but constrained to a standard format to reduce ambiguity. This standard format uses *shall* for mandatory requirements and *should* for desirable requirements. Text highlighting should be used to identity the key parts of the requirement.

The problems with this format are that when a complex but precise idea is put into natural language, it can be difficult to read. Some requirements might also be written better as multiple requirements.

Diagrams can be used to represent the components needed for each requirement, and the relationships between these requirements. They are most useful for understanding dependencies, reasoning about changes of state of the system, and describing sequences of actions.

An *architectural system context model* uses boxes and lines to represent the subsystems and the communications between them respectively. A *process-based system context model* uses round rectangles and arrows to describe processes performed by the system.

These models can be created from the requirements document, and are intended to give the developers instructions on how to meet the requirements and provide a basis for designing the system.

###Modular Decomposition

*Modular decomposition*, or top-down decomposition, is the process of splitting the work performed by the system into self-contained modules. Bottom-up composition the process of combining these modules to create a complete system.

One technique for decomposition is *function-oriented pipelining*. This uses the idea that the modules act as a pipeline through which all the data in the application must pass. Each module filters the data in a certain way. The modular arrangement must begin with a data source and end with a data store.

Advantages of function-oriented pipelining are  
- The role of each module is easy to understand
- Modules which take arbitrary data and transform it can be reused with different data
- The system can grow by adding new sections into the pipeline

Some disadvantages are  
- Communication between modules is limited by data communication rules  
- It will struggle to represent event-driven systems such as GUIs

Another technique is *object-oriented decomposition*. Each module is an object which holds data, processing capabilities and responsibilities for what work it needs to do. Objects are tangible entities in the system (such as 'the address book') or participating agents (such as 'the salesman').

Objects must define their public interfaces that other objects can use to send data to and request data from. They are instantiated from classes.

Advantages of object-oriented decomposition are  
- It is easy to understand the link between a module and the entity it represents  
- It provides encapsulation, improving security and reducing coupling
- Allows for very easy reuse, through inheritance as well as complete reuse

The main disadvantage is that the object-oriented approach is time- and memory-hungry at runtime, which restricts its use in certain situations.

###Unified Modelling Language (UML)

*Object Oriented Development* is a more modern approach to software development. It comprises object-oriented analysis, design, and programming. OO analysis identifies an object oriented model of the application domain, and the operations associated with the problems to be solved. OO design identifies an object oriented model of the software system to implement the identified requirements. Good OO design aims for high cohesion and low coupling. OO programming realises the object oriented software design, e.g. using Java, C++ etc

There are 5 activities in a typical OO design process:
- Define system context and modes of use (e.g. use cases)
- Design the system architecture
- Define the main "objects" in the system (abstraction)
- Construct design models
- Specify object interfaces

There are two basic types of design model. *Static models* describe the static structure of the system, i.e. organisation of components, including models of object classes. *Dynamic models* show the interaction of objects.

*UML* is a set of graphical notations for creating OO software. It can represent both data (attributes) and processes (operations), and was standardised by the Object Management Group (1997). It allows representing and reasoning about software with a very broad scope, as combinations of UML models can represent softare in very diverse application domains. It provides 13 different modelling diagrams, 6 static and 7 dynamic. There are 4 considered in this unit: Class (static), use cases, sequence and state machine (all dynamic).

An *object* is a self contained software entity with well defined characteristics and behaviour. The characteristics are represented by attributes, and the behavours are represented by its methods.

A *class* is a generic definition of an entity, for a set of similar objects. It is like a blueprint for creating software objects.

A *class model* provides a diagram of the static relations between entitites in an applicaton. It shows the key components (classes) and their relationships (associations) within the application.

The typical UML class notation is split into 3 sections; the class name, attributes, and methods. All attributes and methods should have access modifiers (the + or -). A + corresponds to a public variable or method, and - corresponds to private. Attributes must list their type, and methods their parameters and return type.

![](http://i.gyazo.com/84d64e4a540b2aee07537679d02f4196.png)

Associations between classes are denoted by dotted arrows (denotes a 'has a' relationship). These are usually annotated with semantics (e.g. purchases, issued to) and multiplicity. They can also have a hollow diamond instead of an arrow head, which means a one to many relation, or a solid diamond which means one to one. Multiplicity is denoted as follows:
- 0..1 - Zero or one instance
- 1 - Exactly one instance
- 0..* or * - Zero or more instances
- n..* - N or more instances

Class association:
![](http://i.gyazo.com/e3187daeb999105782e7ed56cc99395c.png)

Object classes are often organised into hierarchies, e.g. Cat 'is a' Mammal, which 'is an' Animal. Parent classes have features common to the more specialised classes which inherit them (children). Child classes inherit attributes and operations, and add specialisation as necessary. They can inherit multiple classes (e.g. both 'mammal' and 'predator'). Objects in good class model designs do not inherit unnecessary attributes, and name clashes are resolved meaningfully in case of mu ltiple inheritance e.g. two super-classes both have an attribute 'A'.

In UML class diagrams, inheritance is denoted by arrows with solid lines and hollow heads. Any interfaces which are implemented are denoted by either an arrow with a dotted line and hollow head, or a ball and socket in UML 2.0.

![](http://i.gyazo.com/d8b3a9f14812f44e2a4c10eff46c1f8a.png)

A *Semantic Data Model* can be an Entity-Relationship-Attribute (ERA) diagram, or can use UML classes. If using UML classes, they should have no methods. Below are two semantic data models for a book review website, one using ERA and one using UML.

![](http://i.gyazo.com/ba9f87d04993cbc75dd8144aa187f3c2.png)
![](http://i.gyazo.com/aae3a264fbbeb75b0c549e8884e188bf.png)

Semantic Data Models must always be accompanied by a data dictionary, necessary for name management and storing organisational information.

![](http://i.gyazo.com/4f3c538f6864e13b99430b28995a5d4d.png)

Many behavioural models have been proposed to specify how system components interact with one another. These include data flow diagrams (not UML), state machine models (UML) and sequence diagrams (UML).

*Data flow diagrams* are the traditional approach. They are convenient for describing single threaded data processing systems, as data is transformed to an alternative representation without much interaction between system components.

*Sequence diagrams* are models of how objects implement use cases, and are used to model the interactions between objects. They help designers to specify how particular computations are performed by the system as a whole - which objects 'talk' to which other objects (or subsystems), and in what order. They are directly related to static models. Some features of sequence models are:
- Time runs from top to bottom.
- Objects involved in interactions are listed across the top.
- Thin rectangles show when an object has control. This is handled in nested calls upon other objects.
- Labelled arrows indicate object interactions, not data.

Here is an example of a sequence diagram:
![](http://i.gyazo.com/41a114634498849534370bc8df988491.png)

*State-machine models* are used to design and analyse event processing systems (e.g. real time systems). They are loosely related to static models. At any time, all software systems are in one of a number of possible states - ready for input, processing data, displaying output etc. When something happens, the machine must change state. State machine models show how a system responds to different stimuli. This can be from an external source (e.g. the user) or execution of internal code. They include a graphical diagram, showing states as rounded rectangles and stimuli as arrows, and a descriptive table to give explanations of the different states and stimuli.

Here is an example of a state machine model for a car park barrier, and the descriptive table to go with it.
![](http://i.gyazo.com/dc826f268d2391a28ec8cc9f1837f5b7.png)
![](http://i.gyazo.com/f24ef0f3dc01035d0c429cca0dff5616.png)

*Models* are abstractions of your design, and each type of model shows a particular aspect of the design for a particular purpose. Modelling can take place from a number of perspectives:
- Context Models - Defines boundaries of your system and its dependencies/interactions with it's external environment.
- Architectural Models - Describes your system structure and its components at a high level.
- Semantic Data Models - Describes logical structure of data input/output by the system.
- Behavioural Models - Models the behaviours and interactions of system components.

###Use Cases and Scenarios

*Scenarios* are narrative descriptions of exactly how a user might use the system. They are written in English in paragraph form, and provide a description of the user's interaction with the system. They will describe ordinary and exceptional situations.

An effective scenario includes:
- The starting situation
- The normal flow of events
- A description of what could go wrong
- Information about concurrent activities
- The finishing state of the system

*Use cases* are descriptions of the system as a sum of its possible scenarios. They typically are represented by diagrams of actors and their interactions with system objects. Actors are external entities including users (eg 'customer') and other systems (eg 'the payment database'). Use cases, therefore, identify which functions will be available to which actors and how the system will behave with respect to actor input.

In UML, use cases are represented as a static diagram accompanied by descriptions of the scenarios named. They must be object-oriented and relate to what the user wants to achieve with their interaction.
![](http://gyazo.com/180542551a9a69d4724e8b23d69932ee.png)

Each use case has an associated scenario, and scenarios can refer to each other and common sub-tasks if they are repeated. In a use case diagram, this is shown with a dashed arrow marked include:  
![](http://i.gyazo.com/525ab92dc10b98a34c30731816ca6007.png)  

Individual services should be defined per task from a user perspective rather than relating to the objects in the system. The UML class model should be developed alongside this without having a one-to-one relationship between services and classes.

*Sequence diagrams* are dynamic models used to show the interaction of objects during situations in the running of the program. They show the flow of control and dependencies between objects. They should include *escape sequences* describing how the user would cancel an operation, parallel tasks and an order in which information should be supplied.

The *task-artifact cycle* describes how systems should be developed and then evolve to respond to how they are being used:  

1. People perform a task  
2. Study the people performing the task  
3. Make a model of the task being performed  
4. Make an artifact to support the people performing the task  
5. People perform the task with the artifact. Repeat from stage 2  

###Scheduling

Project planning consists of breaking down the work into parts, assigning these to team members, and trying to anticipate and deal with any problems that arise. It also involves regular reviewing and replanning. Planning is an *iterative* (ongoing) process.

It is important to assess your constraints when planning. Questions to consider include when must it be completed, how much is our budget, who will be working on it etc. You should also define milestones in order to assess the progress throughout the project, with the final deliverable being the last milestone.

Project management can be viewed as balance between time, scope and cost, as seen here:
![](http://i.gyazo.com/14b9bc0a00ef05ac16b6e3a4fdb426be.png)

The project planning cycle goes like this:

1. Project starts, work begins
2. Review project progress
3. Revise project parameters
4. Update project schedule
5. Renegotiate with client if needed
6. Deal with software technical problems if needed (this may involve internal technical reviews)
7. Repeat from step 2 until the project is completed

When scheduling, you should break down the project into a list of activities/tasks. Estimate the time and resources required to complete activities, and organise them into a coherent sequence. Be sure to allow for contingencies when estimating duration. We work in the real world, and problems will always arise, so factor in a % delay using prior experience of similar projects.

When scheduling activities, consider concurrency, i.e. can multiple tasks be completed simultaneously? Also consider dependency - does this task need to be completed before we can start the next task? Activities, milestones and dependencies should be recorded in a table like this:
![](http://i.gyazo.com/06a5d904a04249c915af7b4c01756d5f.png)

A *Gantt Chart* is a tool to represent the structure of the team's work. It is designed to allow planning and monitoring of tasks, and shows the breakdown of the work into tasks over time. The chart gives a clear impression of task timing i.e. what needs to be done by when. Concurrency is clear, however dependencies and personnel responsibilities are hard to see.

Example of a Gantt Chart:
![](http://i.gyazo.com/3763ede55bd0c1cdc9fc5200757e0b16.png)

The *Critical Path Method* (CPM) is another method of scheduling. It is a simple node-and-edge graph of tasks to be carried out with time, and is used to identify critical tasks (possible 'bottleneck' points). The critical path is the longest one from start to finish. It allows project managers to invest more resources into critical tasks to avoid a project slip. However it can be difficult to identify the task start/end times at a glance.

Here is an example of a graph made using the critical path method and it's associated table. The path in red is the longest, and is therefore the critical path.
![](http://i.gyazo.com/d2aacee5d50e56a9ff9b2543fdb9bf6c.png)
![](http://i.gyazo.com/e8dabf1ca5cc0b78f629415b038dc223.png)

###Managing People

Software engineering is a group activity, as real-world big software projects can rarely be completed by one person working alone. Groups are often multi-skilled, so good people managers are able to get the best out of their team. Poor people management is a major cause of systems failure.

*Brooks's Law* states that "adding manpower to a late software project makes it later". This is because it takes some time for the people added to a project to become productive, and also because communication overheads increase as the number of people increases.

Individual group members may bring specific skills to the team, which software engineering companies have to manage and preserve, for example:
- Specific product or application domain experience
- Specific platform or programming language skills
- Skills such as User Experience (UX) and hardware interfacing (these skills are in short supply)
- Problem solving, communication and social skills

There are several factors to consider in people management:
- Consistency - Team members should all be treated in a comparable way without favourites or discrimination.
- Respect - Different team members have different skills, and these differences should be respected.
- Inclusion - Involve all team members and make sure that people's views are considered.
- Honesty - You should always be honest about what is going well and what is going badly in a project.

Motivation is a very important factor in people management, and a fairly complicated one. This *Hierarchy of Needs* by Abraham Maslow models the differenct factors affecting motivation:
![](http://i.gyazo.com/5f49be102c38c2688e2150176fcd8ee2.png)

Individual people are motivated by combinations of objectives and activities. These can be task oriented (the work itself), self-oriented (rewards brought by successfully completing work) and interaction-oriented (being part of a social group and dealing with co-workers). The balance between these can depend on personal circumstances, the size of the team, the degree of individual contact or external events.

Selecting and deploying staff is an important process, as poor groups can cause sytems to fail, and you need to manage and get the best value of of their intellectual capital. Information on this comes from interviewing and talking with candidates, and recommendations and comments from other people who know or have worked with the candidates. Important factors include:
- Educational background and willingness to learn
- Adaptability (range of past projects and activities)
- Positive attitude, enthusiasm and work rate
- Compatibility of personality with the team

*Group cohesiveness* is when group members possess bonds linking them to one another and the group as a whole. Cohesion means that peoples inhibitions to contribute are reduced, and group quality standards can be developed. Group members work closely together, so the team members learn from each other and get to know each other's work.

Cohesiveness is influenced by factors such as the organisational culture and the personalities in the group. Cohesiveness can be encouraged through social events, developing a group identity and territory, and explicit team-building activities. Openness with information is another simple way of ensuring that all group members feel like part of the group. However, cohesive groups may develop very loyal memberships, which is generally a good thing but can also lead to restrictive practices.

*Groupthink* is a preservation of group irrespective of technical or organisational considerations. It is a phsycological phenomenon that occurs within a group of people, in which the desire for harmony or conformity in the group leads irrational or dysfunctional decision making. Group members try to minimise conflict and reach a consensus decision without critical evaluation of alternative viewpoints, by actively suppressing alternate viewpoints and isolating themselves from outside influences. Management should act positively to avoid groupthink, by maintaining external involvement with each group and have multiple group memberships within the company.

Group communication is essential for effective group working, and is the main mechanism for defining and coordinating joint work, and conducting work where more than one person is required. Information must be exchanged on the status of work, design decisions and changes to previous decisions - this in turn strengthens group cohesion.

###Requirement Discovery

**Interviews**
- Unstructured of semi-structured in early scenarios and structured for more specific scenarios
- Gives development team members a chance to meet stakeholders, stakeholders feel more involved
- Collect information on peoples ideas, opinions and experiences

**Focus Groups**
- Establish a consensus view, not just one person
- Highlight areas of disagreement
- Again, dev team meets stakeholders

**Questionnaires**
- Get a wider perspective on an issue
- Or opinions about specific suggestions from a particular audience

**Direct Observation**
- Understand the nature of the tasks and the context in which they are performed
- Can be carried out by trained observers who report back to the design team, or by a member of the design team

**Indirect Observation**
- Diaries, interaction logging etc.
- Provide data about how a task is performed currently - often tightly coupled with the existing system, not helpful for designing whole new systems

**Studying Domain Documentation**
- Good source of info about professional bodies and regulations governing a task
- Should be used with other sources, as they may be designed with particular implementations in mind

**Research**
- Observe and analyse similar products to improve/extend the requirements of your own
- reviews/demos/literature/scientific research/case studies

###Interview Practice
- Decide which users to interview, obtain their consent, decide who will do what and when
- Make a plan for bringing together the data, e.g. indexed and secure archive for the raw data
- Select equipment - static information (notebooks, pens, cameras) or dynamic information (voice/video recorders)
- Prepare a written summary of the interview purposes - goals, what will happen to the findings, how their privacy will be protected.
- Be open minded, avoid pre-conceived ideas, prompt them with questions or proposals, build on the things the say (nouns and verbs...)

1. Introduce yourself, purpose/duration of the interview, explain recording method, gaurantee anonymity
2. Warm up, make first questions easy and non-threatening
3. Main body, present questions in logical order
4. Closure, thank interviewee, signal the end, switch recorder off

###Requirements Classification and Organisation
**User Requirements** - high level description in natural language, with diagrams, of what services the system is expected to provide to users

**System Requirements** - more detailed descriptions, defining what will be implemented. Often called functional specification.

**Functional Requirements** - what the system should do, how it reacts to particular inputs, what it should not do

**Non-functional Requirements** - Constraints on the services of functions offered by the system. Often apply to thewhole system, e.g. timing constraints, speed, size, ease of use, reliability, robustness, portability

Requirements should have these fields:
- Requirement: The name of the requirement
- Number: A unique number that identifies the requirement. Ideal for communication purposes
- Description: A short description of the requirement
- Rationale: The reason why this requirement is needed
- Success criteria: What determines that this requirement has been well implemented
- Level of importance: The importance of this requirement for prioritization purposes. Usually a number between 1 and 5

Decide which requirements should be included in which release. To minimise risk, most important or high risk requirements are implemented first.

MoSCoW - method for prioritising requirements. M - must have this, S - should have if possible, C - could have if it doesn't affect anything else, W - won't have this time, but maybe in the future

###Risks

**Risk** - an unwanted event that may occur with negative consequences. Main risks in SE are cost increases, schedule slippage, quality degradation, organisational

- Reactive - wait for problems then act on them
- Proactive - identify potential problems and act in anticipation

Risk management process:

1. Identify - produce a list of potential risks
2. Analyse/Prioritise - produce a risk assessment with prioritised risk list. Assess likelihood and consequences. Table should contain risk, probability, and impact.
3. Planning - produce a risk avoidance and contingency plan
4. Monitoring
5. Response/Resolution - implement plans to reduce/deal with risk

Boehm's top 10 risks:

1. Personell shortfalls
2. Unrealistic schedules and budgets
3. Developing the wrong software functions
4. Developing the wrong user interface
5. Gold plating
6. Continues stream of requirements changes
7. Shortfalls in externally performed tasks
8. Shortfalls in externally furnished components
9. Real-time performance shortfalls
10. Straining computer science capabilities

###Process Improvement

Approaches to process improvement - process maturity approach, and the agile approach.

Process Maturity Approach:
- Measures the maturity of a process. The maturity reflects the extent which good technical practice and management have been adopted.
- Main goals are to improve product quality and process predictability.
- Is about truly understanding the process, analysing and reflecting on it, and identifying weaknesses and improving accordingly.
- Good for large projects with average developer capabilities, where the process determines the product quality.

Agile approach:
- Focuses on iterative development and reduction of overheads in the process.
- Involves rapid delivery of functionality, and responsiveness to changing customer requirements.
- Is about minimising formality and documentation so more effort can be directed into delivering and improving software products quickly. Faster = more iterations = better product.
- Good for small projects, where the capabilities of the developers is the biggest determinant of quality.

3 stages of the improvement cycle - process measurement, process analysis, process change.

**Process measurement:**
- Goals - what is the organisation trying to achieve? e.g. shorter product development time - rapidity
- Questions - about areas of uncertainty about the goals, e.g. where are the bottlenecks in our current process?
- Metrics - measurements to be collected to answer the questions, e.g. time taken to complete process activity

**Process analysis:**
- The study of existing processes to understand the relationships between parts of the process and compare them with other processes.
- Process modelling - the documentation of a process which records the tasks, the roles and entities used etc.
- Study an existing process and produce an abstract graphical model of the process. Then alayse the model to discover problems.
- Can be done with questionnaires and interviews
- Can be done with ethnographic analysis (obtaining knowledge through observation). Best for in-depth analysis of process fragments, not whole process understanding. This is a prolonged activity, could take months.

**Process change:**
Changes can include
- Introducing new practices, methods or processes
- Changing the ordering of process activities
- Introducing or removing deliverables
- Introducing new roles or responsibilities

Should be driven by measurable goals. Use process measurements once the changes are implemented to assess effectiveness. The 5 stages of process change are:

1. Improvement identification - use results of analysis to tackle quality problems, propose new processes methods and tools.
2. Improvement prioritisation, assess the possible changes to the process and prioritise them.
3. Process change introduction - put the new procedures into place and integrate with other process activities.
4. Process change training - engineers involved need to understand the changes made and how to perform new processes.
5. Change tuning. Monitor the changed process, discover minor problems and modify accordingly.

