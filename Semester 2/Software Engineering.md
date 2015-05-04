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

**Software Processes** are a defined set of activities and associated results that produce a software product. There are several different models e.g. waterfall. Activities common to all software processes are:
- Software specification
- Software design and implementation
- Software 'validation'
- Software evolution

Some key challenges faced in software engineering are:
- **Heterogeneity Challenge** - Building dependable software to cope with the heterogeneity (diversity) of existing computer systems, support structures, and legacy software.
- **Delivery Challenge** - Shortening delivery times for complex systems without compromising on quality.
- **Trust Challenge** - To develop techniques that demonstrate software can be trusted by its users.

**Technical computer-based systems** include both hardware and software. The operators and operational prcesses are not normally considered to be part of the system. They are not self-aware.

**Socio-technical systems** *include* technical systems, as well as the operational proccesses and the people who use and interact with the technical system. They are non-deterministic, and governed by organisational policy.

**Project Scheduling** involves estimating the time and resources required to complete activites and organise them into a coherent sequence. The project should be broken down into distinct tasks, with an estimated duration. Contingencies should be allowed for.

A **Gantt Chart** is used to represent the structure of the team's work, showing the tasks the project has been broken down into over time. It is designed to allow planning and monitoring of tasks. It gives a clear impression of task timing, clearly showing what needs to be done and when and any concurrencies. However, it is not so effective in showing dependencies and personnel responsibilities.

A Gantt Chart:
![](http://i.gyazo.com/a09a559ee3f3f56df6ae65bd38e39718.png)

###Ethics and Professional Conduct

**Codes of conduct** are set by professional bodies or institutions, and are necessary to maintain professionalism. They are typically a set of principles that are meant to guide rather than prescribe. Therefore they are often ambiguous in application and must be used in aid to professional judgement in ethical dilemmas.

An example of ethics in the real world is the US Challenger space shuttle disaster in 1986. There were problems with the O-rings in relation to cold launch conditions, which was noted by an engineer. However, no testing was done due to more pressing problems. The engineers all unanimously recommended against the launch, however Space Centre was "surprised and appalled" at the recommendation, and went ahead with the launch due to political and financial pressures. The O-rings failed and the shuttle exploded 73 seconds into the mission, killing all seven crew.

There are 8 main principles in the **ACM/IEEE Code of Ethics**. These are:

1. Public - Software engineers shall act consistently with the public interest.
2. Client and Employer - Act in the best interests of their client and employer, consistent with the puiblic interest.
3. Product - Products and related modifications shall meet the highest professional standards possible.
4. Judgement - Integrity and independence in their professional judgement.
5. Management - Adopt and promote an ethical approach to the management of software development and maintenance.
6. Profession - Advance the integrity and reputation of the profession, consisten with the public interest.
7. Colleagues - Be fair and supportive of other colleagues.
8. Self - Software engineers shall adopt both a "lifelong learning" and ethical approach to the practice of their profession.

There are many potential difficulties with codes of conduct. They can be ambiguous, parts of it may conflict, and you may find yourself in situations which are not covered by the code, in which case you are expected to behave professionally and use your best judgement. Codes of conduct are also subject to continual development.

The **B.C.S. Code of Conduct** (revised 2011) is as follows:

1. **Public Interest**. This takes into account public health, privacy, security and well-being of others and the environment. It also covers legitimate rights of third parties, and discrimination on grounds of sex, sexual orientation, maital status, nationality, colour, race, ethnic origin, religion, age or disability.
2. **Professional Competence and Integrity**. Do not claim to be competent when you know you are not. Develop your professional knowledge and skills (lifelong learning). Respect and value alternative viewpoints. Reject bribery.
3. **Duty to relevant authority**. Respect confidentiality of information unless the law requires disclosure. Avoid conflict of interest between work and relevant authorities.
4. **Duty to Profession** Uphold the reputation of the profession. Encourage and support fellow members in thier professional development.

The **UK Computer Misuse Act** supports prosecution of computer related crime. A person if guilty of an offence if he/she causes a computer to perform any function with the intent to secure access to programs/information on any computer, and if that access is unauthorised (and he/she knows this at the time). Causing unauthorised modification of a computer material is a more serious offence. It doesnt matter where the access was made from, or whether the offender is a British citizen.

###Models of Software Engineering Processes

A **software process model** is an abstract representation of a process. It presents a description of a process from some particular perspective. It is a simplified version of reality, and is useful for planning and managing SE projects.

The **waterfall process model**:    
![](http://www.cs.odu.edu/~cs333/website-latest/Lectures/waterfall/page/waterfall0.gif)

In the waterfall model, specification precedes development. One phase has to be complete and officially signed off by the client before moving onto the next phase (sign off means that the SE team won't go back and improve or redefine earlier work). This is suitable for projects that have 'change proof'requirements, e.g. large multi-site engineering projects, stable business environments. This creates a very clear project management model, with easy allocation of responsibility and milestones at the end of each activity. However it is difficult to respond to changing requirements - few business systems have stable requirements, and the clients operations may change too.

Another process model is **formal development**. A waterfall-like process is used, with a formal specification (uses logical notation). However it is refined through several transformations to a design that can be implements.

**Iteration** is very important in process models. There is almost always pressure to change system requirements in the course of a project - This means results of earlier activities must be reworked, and implications for later activities must be considered. This produces unpredictable results unless managed. Iteration can be applied to any of the generic process models, but is hard to do effectively. However, some special process models have been invented to systematically handle iteration.

**Incremental software processess** have development and delivery broken down into increments, where each increment delivers useful service. Requirements are *well defined and prioritised*. High priority requirements are frozen and included in earlier increments. Requirements for later increments can continue to be defined whilst earlier increments are constructed. This model means that users gain immediate value, as the highest priority services are delivered first, so they dont have to wait as long for useful services. There is also a lower risk of project failure, because it is unlikely that no increments will be delivered, and high-priority services are completed first and therefore receive the most testing. Users can also gain experience from early increments as prototypes, improving requirements for later increments.

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

An example of an agile software process model is **eXtreme programming (XP)**. The client is part of the development team, and new versions may be built several times a day. Requirements are simply 'story cards' developed from user scenarios, and the test-first approach to development reduces the chance of new increments introducing errors into the existing software. This uses scripts for automated testing. It also features par programming on shared workstations, which leads to constant informal reviewing and promotes refactoring. However, this can be perceived as constraining and invasive, and it requires a small co-located team that are happy to do pair programming.

Abstract model of a generic cycle with the XP proccess model:
![](http://i.gyazo.com/87571ddedce23b445b7ccfbd26d41ff0.png)

The **spiral model** is a software process represented as a spiral, rather than a sequence of activities with backtracking. Each loop in the spiral represents a phase of the software process. Risk are explictly assessed and resolved throughout the process. There are no fixed precossese e.g. specification or design, and loops in the spiral are chosen as required. There are four sectors of the spiral model:
- Objective setting - specific objectives for the phase are identified.
- Risk assessment and recution - risks are assessed and activities put in place to reduce key risks.
- Development and validation - a development model for the system is chosen which can be any of the generic models.
- Planning - the project is reviewed and the next phase of the spiral is planned.

Abstract model of a generic spiral model:
![](http://i.gyazo.com/87f8424666b35aa269a5e8dd08e878b3.png)
