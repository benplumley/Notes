#CM10228 - Programming
##Dr Joanna Bryson

###Languages  
All programming languages run on physical computers, take time to run, take space in memory, and run algorithms. The amount of time and space a program takes to run is known as the program's *complexity*. Algorithms with lower complexity are better.

The *Church-Turing thesis* says that any algorithm can be run on a Turing machine. All computers are Turing equivalent, and every real programming language is Turing complete. An algorithm is defined as something that can run on a Turing machine.

Languages can be *compiled* or *interpreted*. Compiled code is turned from human-readable code to machine code long before being run, interpreted code is evaluated line by line. Compiling means the program will run faster, but the compiled code will be less transportable between different computer architectures.

Languages can be *strictly typed* or not. A strictly typed language defines the data type of a variable when that variable is created, and only allows objects of that data type to be assigned to that variable. Non strictly typed languages do not associate data types with variables; the data type of the variable is simply the data type of the object currently assigned to that variable.

Languages can be *object oriented* or not. An object oriented language allows any piece of code and data to be defined as an object that can be instantiated and passed around.

Languages can be *high* or *low level*. A high level language is closer to being human-readable, and tends to be more verbose. A low level language is closer to being understood by a computer, and tends to be more compact.

Languages can be *dynamic* or not. A dynamic langauge can write and evaluate (run) new code whilst currently running. For instance, a program could contain a text box accepting code in the language it is running in that would then run as part of that program.

In the real world, not all languages fit these binary definitions. Java, for instance, is partially compiled and partially interpreted, strictly typed, object oriented, high level, and partially dynamic.

###Data Structures  
Arrays of primitive data types are chunks of adjecent memory locations. Arrays of objects are arrays of references to other memory locations containing the objects in the array. An item in a list is made up of two references, one to the object at that position and one to the location of the next item in the list. The "next" reference of the last list item is null.

Arrays are faster when the array length is known ahead of time. This is because accessing the nth item in an array is a constant complexity operation; it takes as long to find the object at position 100 than the object at position 1.

Lists are faster when the length isn't known or is likely to change. To change the size of an array, a new block of memory the right size must be found and the old data must be copied into it. To change the size of a list, the pointer of the last item must be changed to that of the new last item. However, accessing the item at position n in a list is a linear time operation; accessing the object at position 100 might take 100 times longer than accessing the item at position 1.

Lists also make it easier to add a new item into the middle - in an array, the last half of the array would have to be moved and the new item inserted into the space. In a list, only the item immediately before the one being added must have its pointer changed to point at the new item, then the new item can carry on the list by pointing to the next one.

In modern computers, the time taken to complete these operations is negligible in most cases.

The language *Lisp* implements lists as described here. The reference to the object is called *first* and the pointer to the next list item is called *rest*.

###Sorting and Searching  
Sorting is useful because it makes searching faster. A sorted list can be searched with a binary search in logarithmic time, an unsorted list must be searched item by item in linear time. It is therefore useful to common applications of searching to sort the list first.

Artificial intelligence can be generalised to a problem of searching a list of things to do for the best one, and this must be performed quickly otherwise the conditions specifying what a good thing to do is may have changed by the time an action is chosen.

Items in a list are sorted using a key. This is a piece of the data that is part of the list item. For instance, the key to sort a dictionary is the word to be defined. The key to sort a phone book is the name of the person. Choosing the key is sometimes non-trivial; it should (or must) be unique, have a sensible order (eg numerical, alphabetical, chronological) and be the part of the object that is already known. A phone book ordered numerically by phone number would be useless.

*Selection sort* can use two arrays. The first array is iterated through to find the smallest item, which is inserted into the first position of the second array. This is repeated until no items are left in the first array. The second array is now in order.

Alternatively, this can be done with a single array, instead of putting the smallest item into the first position, the smallest item and first item are swapped. This requires an extra temporary variable for storing the value of the item being swapped.

**Selection sort is O(n^2).**

*Insertion sort* splits the array into sorted and unsorted parts. Initially, the sorted part contains only the first item of the whole array. Then the first item of the unsorted part is inserted into the correct position into the sorted part and removed from the unsorted part. This is repeated until the unsorted part has no elements.

**Insertion sort is O(n^2).**

*Quick sort* chooses a number (typically the one in the middle of the array) as the pivot. All numbers smaller than this pivot are put into a new array to the left of the pivot, and likewise with larger numbers to the right. This is then repeated recursively on the new smaller arrays. When all arrays contain a single element, putting these back into a single array in the order they are currently in will result in an ordered list.

**Quick sort is O(n log n).**

*Bubble sort* starts at the first element, compares it to the second, and swaps them if they are out of order. It then repeats this from the next element. Once it has passed through the array it will have carried the largest number to the end of the unsorted area, and into the sorted area. The process is then repeated from the start of the unsorted area.

**Bubble sort is O(n^2).**

*Merge sort* splits the array in half recursively until each array has only one element. These arrays are then merged two at a time, sorting the items into the correct order at each merge.

**Merge sort is O(n log n).**

Algorithms which solve their problem by splitting the input in half recursively, such as quick sort and merge sort, are known as *divide and conquer* algorithms.

###Algorithmic Complexity  
Algorithms are evaluated based on their speed, size, risk of failure and ease of maintenance. The complexity of an algorithm typically is referring to its speed, but could also mean size. Due to the speed of modern computers, a slower but easier to maintain algorithm might be preferable because the computer's time is cheap compared to that of a programmer to maintain it. However, in situations where the result is needed quickly such as when rendering in a game engine, the speed of the algorithm is more important.

Speed of an algorithm is measured by counting the number of basic operations the algorithm performs. More importantly, the complexity is a measure of how this number of basic operations changes as the amount of input data the algorithm is processing changes. This is known as the *scaling* of the algorithm. This scaling happens with respect to some independent parameter. For a sorting algorithm, this parameter is the number of items to be sorted.

An algorithm is called *fast* if it grows quickly, so a *slow* algorithm is better. In order from slow to fast, algorithms can be constant, logarithmic, linear, quadratic, polynomial, exponential, or factorial.

A *binary tree* is like a list, except rather than each item having one pointer to an object and one pointer to the next item, it has one to an object, one to the child "right" of it and one to the child "left" of it. Finding an item in a binary tree is log 2 complexity.

*Big O notation* is used to record the complexity of an algorithm. The number of operations as a function of n (problem size) taken, and all terms other than the dominant one are removed. This is the big O complexity of the algorithm. For instance, an algorithm running in 2n^3 + 18n + 5 steps is O(n^3), or polynomial complexity.

Algorithm complexity can be evaluated for the *worst case*, *best case*, or *average case*. In the worst case, the input data is presented in the worst possible way. For instance, a giving a bubble sort a list of items in descending order to be sorted into ascending. The best case is the best possible set of input data, for instance giving it a list that already happens to be sorted. The average case is the most likely situation to happen in practice.

Technically, big O notation is used for the worst case, but it is often used for average case instead.

Once a list is sorted, a binary search can be used instead of a linear search. This is a divide and conquer algorithm, so takes log n time. This can be improved on using *hashing*. This uses the key as the array index. For instance, to find the student with ID 567, the algorithm accesses the item at position 567 in the array of students. This is O(1), or constant, time. This array can be sorted in O(n) time. However, this assumes that the key is unique. If this is not true, each array item will need to be a list of objects with that key.

This also means that contiguous memory is needed for every possible key between the first and the last one. A dictionary arranged in a hash would be almost completely unused space, because every combination of letters of a reasonable length would need its own entry, whether it had a definition or not.

The solution to this problem is a structure called a *hash table*. This uses an array that's about the right size to contain every element. The key is turned into the index array using the *hash function*. This function must be simple and fast because it must be performed on every access. For instance, the hash function could be the index mod something. Multiple items could have the same hash, so each location in the hash table contains a list of items with that hash. This is known as *chaining*.

In the best case, where each cell contains a single element, searching for an element is O(1). In the worst case, where all elements share the same hash, finding an element is O(n). Therefore, the more collisions that occur, the longer it takes to find an element on average.

If the table has more cells than elements, a technique called *probing* can be used instead of chaining. Rather than putting a list of elements in each position, any subsequent elements after the first in each cell are put into the next empty cell after the one they are supposed to go in.

The time to find an element in a hash table depends on not how many cells or items it contains, but how full it is:  ![alt-text](http://upload.wikimedia.org/wikipedia/commons/1/1c/Hash_table_average_insertion_time.png)

*Polymorphism* is applying the same method to different objects. There are several types of polymorphism. *Overloading* is where multiple methods in the same class have the same name but have different parameters and signature. *Overriding* is where a subclass redefines a method inherited from a superclass. This will have the same signature as the overridden method. *Dynamic binding* is where a method is called on an object, but that object's type isn't known until runtime. For instance, calling a method on each object in an array, where each object isn't necessarily of the same type.

*Class variables*, or static variables, are variables whose values are consistent across any object of that class. The memory assigned to these variables is low on the stack so it stays there the whole time the program is running.

In Java, Class is a class. This is instantiated to make every class, and contains methods such as getClass to get the class name of an object.

###Threading  
Simplistically, programs execute sequentially from the first statement to the last. The program counter keeps track of the current line number. *Non-linear flow of control* is the deviation from this sequential flow introduced by statements such as goto and loops. In Java, *break* and *continue* are used in loops to change the flow of control. Break jumps out of the current innermost loop, or to the label if one is used. Continue skips all the remaining code in the current loop and goes back to the start of the next iteration.

When a process dies or is killed, it is unsafe to simply stop its threads from running. To exit cleanly, a program must close any files it has open and give up any other resources, and kill any children it spawned. It will probably want to save its state to disk.

###Exceptions  
When something goes wrong in many programming languages, the program is said to throw an exception. The routine for dealing with this problem occurring is said to catch the exception.

In Java, *throwables* are errors and exceptions. They are full objects which can be instantiated and passed around. An *error* is something that can't be solved by the program whilst running, such as syntax errors. An *exception* are things that the program may be able to solve whilst running.

Exceptions are further split into *checked* and *unchecked*. Checked exceptions must be caught and dealt with in order to compile. For instance, lots of IO operations can't be called without catching their possible IOExceptions. Unchecked exceptions mean the programmer has made a mistake. These don't have to be caught, but can be.

Checked exceptions must be put inside a try clause, followed by a catch clause containing code for handling that particular exception. Finally clauses run after all other clauses.

Throwing a checked exception can be done by creating a new Throwable and using the throw keyword. Methods which throw exceptions and don't catch them must instead *propagate* them, or pass them up to the calling method. A method's ability to do this must be included in the method signature.

Throwing and propagating unchecked exceptions is done automatically and implicitly.

Computers are able to run more programs than they have concurrent threads in the CPU. As well as all the user programs, emails are being checked, virus scans are running, the clock is changing, and so on. A single CPU only runs a single process at a time, so to perform all the tasks it has, a computer must very quickly switch between different processes.

Different tasks are given different priorities depending on how important it is that they execute soon. Clicking the mouse is something that is given very high priority, so the user does not experience a delay after having clicked something. Background tasks are only run when the computer would otherwise be doing nothing at all.

Because swapping control between two processes takes cycles, a balance is found between swapping rarely - possibly causing the computer to feel unresponsive - and swapping often, which wastes cycles that could otherwise be used for processing.

Any program that takes input from the user spends most of its time doing nothing, because thousands of cycles can elapse even in between key strokes.

A single program can have multiple processes. For instance, a program that has a GUI for control and performs processing of data needs at least two threads, otherwise the GUI will be unresponsive while the data is being processed.

The original way of creating a new thread was called spawning, and was used by calling fork within a program. This would create a clone of the currently running process, and return a different value to each version. All code intended to be performed by the child had to be inside a conditional on this value, and vice versa for the parent.

A more modern approach is called threading, which is what Java uses. Threads created within programs are not copies of the original program. Depending on the OS, threads created will be *kernel threads*, which are efficient and fast. If the OS does not support these, the Java VM will create a thread independently of the OS called a *user thread*. These are not as efficient and slower. There is no difference in how programs are written, only how quickly they run.

There are three ways to create threads in Java. The first is to write a class extending Thread, create an instance of it and call start on it. The second is to write a class implementing Runnable and do the same. The third is to write an inner class, which is the dominant method when creating GUIs.

Threads run independently of one another, but they are still able to interact. Class variables set in one thread are accessible in another of the same class. Multiple threads in the same object share instance (global non-static) variables.

The OS or VM gives each thread a time slice, and the thread will run in that slice until its time is up or it yields. It could also become blocked, put itself to sleep, wait for an event, or terminate.  The states a thread can be in are therefore new, ready, blocked, running, dead, or inactive.

A new thread becomes ready when start is called, and becomes running when run is called. There's no guarantee about which order different threads will be run in, it's down to the OS to pick a thread and which gets picked isn't predictable by the programmer.

Threads will become dead after finishing and dropping out the end of their code. They can also die after receiving an interrupt. This is a polite request for the thread to die, hence why some programs (eg ping) can print a summary after the user presses ^C to interrupt. The thread is in charge of how it dies, it is not forcibly killed by the operating system. Therefore, a thread could refuse to die at all when it receives an interrupt, in which case a different termination signal would have to be sent.

It is down to the programmer to check for interrupts in the run method. If a program hangs waiting for IO, the interrupt request is handled by the VM or OS, but if the program is stuck in a tight loop (a loop which has been compiled to run very quickly) then interrupts should be checked for explicitly by the programmer.

The problem with two threads sharing access to a class variable is if both try to change it at the same time, only of the changes will be registered. The solution to this is to lock variables that need to be changed by a thread. If another thread tries to access the locked variable, it will block as if on IO until the variable becomes unlocked and the blocked thread is rescheduled.

In Java, a lock is called a *semaphore*. Each object has exactly one lock, which can be held by one thread at a time. If a thread does not hold an object's lock, it can't edit that object. Locks should be held for as short a time as possible.

Locking in Java can be done implicitly using *synchronisation*. By declaring a code block or method synchronized, only one thread can call the code within that block at a time. Any other threads will be blocked. Synchronising a code block takes an argument, which is the object whose lock is to be synchronised with. For synchronisation to be effective, this object must be shared between any threads that could call this code block. It is pointless to synchronise on a local variable.

Deadlock occurs when a circle is formed of threads waiting for a locked object, where each object is locked by the thread next to it in the circle. This can be solved by requiring locks to be acquired in a certain order, but this is inefficient if a process needs a new lock that comes lower in the order than the locks it currently has. It also depends on the programmer to implement this properly. If the programmer makes a mistake, the program can still deadlock.

Another solution to deadlock is to have the scheduler or other OS process look for processes which haven't done anything for a long time and interrupt them. This will release their locks and allow the other process to acquire them and finish. However, it means the interrupted process didn't finish what it was doing, which might have been important to the running of the program.

The main way to avoid deadlock is by carefully designing the program to not have the possibility for it to happen, through use of good design patterns. Using synchronised code too much means that most of a process' time is spend blocked. The amount of time a process spends running compared to blocked is known as its liveness.

Unless specified by the programmer, a new thread is grouped with its parent. This means it inherits certain attributes, such as which files it is allowed to manipulate, its priority when scheduling and its niceness.

Livelock is similar to deadlock, except rather than being blocked, the threads immediately go back to sleep after waking up because they can't do anything. This is harder to detect and has to be solved by the programmer during program design.

The *producer/consumer pattern* allows for two threads working at different rates, where one creates data and the other processes it. This pattern uses wait and notify to allow the faster thread to not fall over when it runs out of data to process.

Any object that implements Serializable is able to be written to a file or over a network. When sending data over a network, more can go wrong because routers can drop packets if their load is too high, and phone lines are noisy. Data sent over a network is therefore made redundant, and error-checking code is standard in the protocol.

It is more efficient to have one computer specialised to a certain task than to replicate that functionality on all machines that need to perform that task. This is because a computer might not be running all of the time, which is bad for business because if it isn't running then it isn't making money. This is the basis for the *client-server* architecture. Having one server specialised to a task and clients which are able to request that server perform its task on data sent from the clients means that the server can be fine-tuned to be running as close to all the time as possible. It also means the client machines can be simpler and cheaper.

Some use cases also require a server to be used because the same data is needed by multiple clients. Web servers, for instance, must serve the same web page to any client who requests it. The use of servers to provide processing is known as cloud computing, but it has existed as a pattern since long before the current cloud computing movement.

The differences between a client and a server are that the server starts first, and a server can connect to multiple clients. Once the server has started and made itself available over the internet or local network, it waits for its first client to arrive. When each client arrives, a thread is started for that client which creates a connection through which the server and client can communicate for the duration of that session.

Sockets are the most basic networking concept in a networking-capable language. They provide a door between a program and the network the computer is running on, allowing a program to send data through a pipe over a network. A program will have one socket per connection, so a typical client has one socket and a typical server has as many sockets as it has clients connected. Sockets on the client side have a one-to-one mapping with sockets on the server side. Once connected by a pipe, output from one program becomes input to the other and vice versa.

To connect programs over the internet, an address and port number are needed. The address specifies which machine the other program is running on, and the port number specifies which program to connect to on that machine. A program will typically only listen on one port, so connecting to the wrong one won't allow the machines to communicate.

A *buffer* is a piece of memory that holds a value that will be written to somewhere else. This is because storage is slow, so a process would waste time by waiting for its data to be written to storage. It instead writes its data to the buffer, which is fast, and another process comes along later and writes the contents of the buffer the correct location in storage or on the network.

Standard services, in theory, run on all servers and are publically available. For instance, a client could send a request to any server for the current date and time and the server would respond. Nowadays, these services have been turned off on most servers for security reasons. Standard services have standard port numbers, so they will be the same on any machine.

The telnet program allows the user to type messages to be sent directly to a port on a machine, and if the user types the correct protocol the server might not even know that it's talking to a human rather than to a program.

A *protocol* is a pre-agreed set of procedures for communicating between two computers. It must be followed exactly or the receiving computer won't know what to do with the data being received. A computer can use lots of different protocols depending on who it's talking to and what type of information is being exchanged.

The OSI model defines the layers data travelling between a program and the internet should pass through in an internet protocol. The layers are *physical*, *data link*, *network*, *transport*, *session*, *presentation*, and *application*.

The physical layer describes the physical connection medium, such as the type of wires being used, as well as what electrical signals on that wire mean what data. For instance, a 1 could be represented by a high or a low, or a change up or a change down. It is decided by the physical layer which method is used.

The data link layer sends the frames of data over the physical layer. It is responsible for adding hardware address headers, controlling the rate of flow of the data and checking for errors.

The network layer describes how to forward packets to the next hop in the journey, and so adds the physical address headers for source and destination.

The transport layer describes a single connection between two hosts which can be written to and read from as a data stream.

The session layer describes a single session between two hosts.

The presentation layer describes the syntax of the data, to define what byte values refer to what data types.

The application layer describes what data should be sent, and where to display the information that is received.

An alternative model is the Internet Model, which has four layers. The TCP/IP model fits roughly into the seven-layer model, skipping the presentation and session layers.

The higher layers are typically more human-readable to make debugging easier, and the lower layers are more compact and less human-readable to allow them to be sent over networks efficiently and redundantly. The physical layer, for instance, deals only in single bit values and electrical signals.

Java's sockets provide a connection-oriented protocol with error checking. Java's connections use TCP/IP.

The internet was invented by Larry Roberts and Tom Merrill, who connected a computer in MIT to one in Stanford in 1965. They invented the idea of splitting the data into packets. Their research was funded by the US military and was intended to allow the US government to survive a nuclear war. This is why it was so important for it to be decentralised, so that communications between any points in the country would still be possible if a major city was destroyed.

Internet IPv4 addresses are made up of four 8-bit numbers, allowing 4 billion unique IP addresses. This isn't enough for everyone, so the switch is slowly being made to IPv6 addresses.

Getting a packet to the right destination is divide and conquer, because each router only has to worry about matching one of the four numbers. When the first is matched, the routers will try to match the second, and so on. By the time the last one is matched, the packet is at its destination.

Intelligence, by one definition, is the ability to generate appropriate behaviour in response to an unpredictable environment. An agent is something that can cause change in its environment. Intelligence is more than agency.

Behaviour is the interaction between an intelligent agent and its environment. This could mean physical changes caused by the agent as a result of a change in the environment, or just a change of state of the intelligent system.

Intelligence can also be thought of as choosing the best action from a list of available actions, or choosing to do nothing until a better action becomes available.

There are two processes going on when an AI decides what action to do. It must generate a set of suitable actions, and test each one against some objective function. If it can consistently generate the best action on its first attempt, there's no need to test. If the testing procedure is fast enough, it can generate randomly until it generates something good.

Humans don't consider every possible action at every moment, we only consider a subset of them. This subset is generated based on our previous experience of being in that environment, or the actions of people we've seen acting in that environment. We can then elaborate from the good actions we identified.

Both generation and testing can be thought of in terms of search algorithms. In games, by looking a certain number of moves ahead, an AI can search through many (even all) different combinations of moves to see which one gives it the best result. It can then take the first step towards this combination.

Most AI problems are NP-hard. It is computationally intractable to find the absolute best solution. However, if a potential solution is found, it can be verified correct in polynomial time. If a problem is polynomial time or easier, it's nearly always possible to write an unintelligent algorithm to find the solution rather than using AI. However, there are still cases where AI is preferable.

Depth first search looks all the way to the end of each branch until it finds a solution. Breadth first search looks across every branch at one depth, and if it doesn't find a solution, it moves one level deeper and repeats.

Depth first search is faster, but doesn't give the optimal answer unless the entire tree is searched. Breadth first search guarantees that when the answer is found, it is the best answer in the tree, but isn't possible in cases like chess because of how much memory would be needed to store the state of the tree. Depth first search can enter an infinite loop.

Heuristics can be used to make the process more efficient. In some games, a minimax search can be used. This is true of any game where a move that helps one player must by definition hurt the other player. With minimax, branches that hurt the AI on its turn or help the AI on the opponent's turn can be discarded as bad moves, so the trees under those moves don't have to be searched.

A heuristic search makes an estimate of the value of each branch, and searches those with the higher estimate first. The estimates are based on heuristics, which are metrics from previous experience which give a reasonable estimate of the value of the branch. For instance, in chess, the heuristic could be how many pieces of each type each player has left. While it's not a guarantee of a good branch (they could be awkwardly positioned) it gives a reasonable estimate of the value of each branch.

A* search is a type of breadth first search which sorts the list after every move and chooses to explore the best value path first. If the heuristic can be guaranteed to never underestimate the cost of a branch, A* is guaranteed to give the optimal solution. This algorithm is used in most computer games for pathfinding.

Most languages are capable of using windows to make applications with GUIs. One of the reasons Java is popular for this is that the widgets it uses to create its windows are platform-independent. A Java GUI application created in Windows will be equally usable and equivalent in appearance across OSX, Windows and Linux. This includes matching the look and feel of that operating system.

The original Java windowing system was AWT. Its successor was Swing, but modern applications still use some components from AWT.

The standard system for making a GUI application is called MVC, for Model, View and Controller.

The model contains the functionality and data required for the program. It should contain all the program's algorithms and data structures other than those used to create the GUI.

The view describes how the program will look on the screen. It contains all the objects needed to display on the screen, such as the widgets. Different people could use different views that use the same model, which might allow different options and data to be seen.

The controller connects the view to the model. In Java, this is done using a Listener. Performing actions in the GUI generates events, which are handled in the controller, which calls the appropriate methods in the model.

Top level containers in Java are *frames* and *dialogs*. Everything that appears as part of a Java program must be in one of these. Normal windows are frames, and dialogs are popup boxes that typically appear over frames to give information or ask questions.

Layout managers define how content is layed out within a window.

Languages are invented to fill a need in the market; they tend to do one thing better than anything else available.

Lisp machines were technically very capable computers. They were easy to program, ran a good language, and had a good development environment. However, they were inefficient compared to machines running languages such as C, so lost market share. An efficient version of lisp was created by Lucid, but its development environment was hard to use so its market share kept declining.

Java was written by Sun, which was a hardware company. Their computers ran Unix, and most software was being written for Windows. This was hurting their market share, so their plan was to make Java so that programs written for Windows were also usable on Sun machines.

Microsoft attempted to *embrace, extend, extinguish* this plan as they had done before with internet standards. They wrote a Java VM that supported more functionality than Sun's. Programs written for Microsoft's VM were still Java, but wouldn't run on a Sun machine. Sun programs would still run on Windows.

Microsoft was taken to court twice over this. The first lawsuit was brought by the US government over anticompetitive behaviour. Microsoft were found guilty. The second lawsuit was brought by Sun, which Microsoft settled out of court. This settlement included discontinuing their Java VM.

Monopolies are not inherently a bad thing, as long as the company holding the monopoly does not become anticompetitive. If a company uses its dominant position to hurt its competitors as Microsoft did, this is anticompetitive behaviour and illegal. It is also bad for society, because if only one company has all the money in a field then progress in that field will stagnate, and no new advancements will be made.

Intellectual property rewards innovation in a field. If anybody could sell someone's invention, inventors would be unable to support themselves financially and there would be far less incentive to solve problems.

Copyright is given automatically to literature, films and music, and expires up to 70 years after the author's death, although this keeps changing.

Patents apply to a solved problem rather than a program or piece of code. If someone has a patent on how to solve a problem, nobody else can release a competing solution to that problem for 20 years. This is a relic from the era when patents applied only to manufacturing, when 20 years was a reasonable time to see a return on your investment in factories and production lines.

If a problem is patented, solutions to it can be made but only used in academia until the original patent expires.

Discoveries, including mathematical equations and algorithms cannot be patented or copyrighted. All software was originally considered to be an algorithm, and therefore not patentable. Companies worked around this restriction by turning their software into a physical logic circuit and patenting that instead.

The copyleft movement, created by Richard Stallman, says that the service of writing programs should be sold rather than the algorithms written. Once a program is written, it has no owner. This wouldn't allow for companies the size of Microsoft, but it is still possible to make a reasonable amount of money using only copyleft licenses.

One of the defining features of a copyleft license is that any software that includes a piece of copyleft code must itself be copyleft. This means that a company can't make money from a program if it includes any copyleft code. Not all free software is copyleft.

Initially, it was very important that applications matched the theme of the OS, because so many of the end users were inexperienced enough that a slight deviation from the design could confuse them. The AWT used code native to the OS, meaning programs written with AWT were fast and looked just like the OS they were running on. However, they weren't portable between operating systems, which was their fatal flaw.

Applets are Java programs designed to be embedded into webpages and executed automatically by the browser. Netscape, the dominant browser maker at the time, agreed to support applets using AWT, forcing Microsoft to do the same to be competitive. When Java released Swing, however, IE was dominant and Microsoft refused to support it.

Swing uses no native code, so is completely portable between operating systems. It also fixed a lot of bugs present in AWT. It is the a large part of the reason Java has stayed popular after the decline of applets.

An applet is part a web page. It owns a rectangular section of the page in which it read keyboard and mouse input. Applets essentially allow webpages to run arbitrary code on a computer without (in theory) confirmation, which is why they are blocked by default in modern browsers.

The Applet class contains four methods:  
1. init() is analogous to a constructor. Applets do have constructors, but they are called too early to be of any use to the programmer.  
2. start() is called when the applet is loaded or scrolled into view.  
3. stop() is called when the applet is scrolled out of view. It should be used to stop the applet when it can't be seen, but this is up to the programmer.  
4. destroy() is called by the browser when it's finished with the applet.

If allowed to run, untrusted applets are prevented from reading or writing on the host, opening sockets other than to the server that served the page, starting processes, and running native methods. Applets can bypass these restrictions if they have a valid signature.

Parameters can be passed between the webpage and the applet using tags to send parameters to the applet and methods for the applet to get data about the HTML.

When an AI is searching for an action, it must decide how far to look ahead in its tree of possible actions. For instance, if a chess AI tries to look all the way to the end of the game, it will take far too long to be practical, and run out of memory. Instead, it could choose to look a certain number of moves ahead. A more sophisticated concept is an anytime algorithm.

Anytime algorithms, if interrupted, will give a solution to the problem. If left to run, they will keep searching to improve on their current best solution. This means the time the algorithm takes to run is no longer a variable but a constant if that suits the program. It could also mean that the algorithm is started preemptively and only stopped when the time comes to make the decision.

A *Production Rule System* is an AI that uses productions, which are preconditions related to a certain action. To choose an action, the system will go through its list of productions to find one that evaluates as true. It will then execute the relevant action.

However, many productions are likely to be true simultaneously, so the system must be able to choose which production takes priority. To do this, it must use heuristic rules such as *recency*, which prefers productions most recently matched, and *efficacy*, a measure of that action's previous success rate. Both of these require the system to learn from its past actions.

An *Expert System* is a production rule system designed to encode the actions of human experts in a field. This is hard, because human experts don't store their knowledge as a strict set of productions and actions. They are also capable of learning new actions and productions, something not inherent to production rule systems.

In any learning AI, there is a tradeoff between what is programmed into the AI and what is learned on the fly. The pre-programmed knowledge is analogous to instinctive knowledge contained in our genes, created by evolution.

Learning is a kind of search, only rather than it being performed when the decision needs to be made, it is performed in advance. The programmer includes variable parameters and how they change. When the AI experiences its environment, it sets the parameters according to how they were defined to change.

Some problems are impossible unless the AI can learn, and others are more efficient to learn than they are to program.

An AI can be made aware of its environment by giving it a representation. There are several kinds of representation:  
- No representation. Called *environmental determinism*, the AI responds to inputs (eg I can't move any further in this direction so I will turn) without recording information about its environment.  
- *Deictic representation*. A minimalistic reference that can change depending on the action being taken. The AI only records the information relevant to the action it needs to take, so rather than "the tree" or "player 2" it just records "an obstacle" or "the enemy".  
- *Specialised representations*. If the environment is well defined, this representation has a special-purpose memory which will fit its environment. For instance, our coursework bot memory.
- *General purpose representations*. These are capable of storing arbitrary information. When applied to too complex a problem, combinatorics becomes a problem and these are too inefficient to be of any use. They are useful in specific situations.

A robot is defined as something that generates actions in the real world based on its perception of the real world. This includes things as simple as thermostats. Intelligent behaviour is defined by these interactions, so a robot's physical structure is as important as its control.

A *moral agent* is responsible for its own behaviour. Adults are moral agents, young children are not. *Moral patients* are things we have a moral obligation towards. These might be moral agents, or they might not even be agents. For example, the environment is a moral patient because we have a moral obligation not to damage it but it does not have agency.

The question of whether robots can be moral agents is an open question. One argument is that since humans create AI, we should keep our moral agency and not pass it to the AI. This would mean the behaviour of the AI is the responsiblity or 'fault' of its creator.

*Parallel search* is the use of multiple threads to search through possibilities of actions. Every time there is a branch in what needs to be searched, a new thread is spawned so that no branch has to wait to be searched. With enough processors, all NP problems could be turned into P problems. The number of steps taken to solve a chess game would be the number of moves in that game, so searching them would be near instantaneous. However, there are multiple problems with this in practice:  
- Even very large parallel computers only have thousands of processors, not enough to make a dent in a problem like chess  
- On a normal PC, parallel would have no advantage because the different threads would have to wait for each other to get time on the processor  
- When a thread does find the answer, it must communicate this somehow to every other thread, which is still an open problem with concurrency  

Quantum computing is an experimental branch of computing intended to solve NP problems, and it has been done for small numbers of qubits. A specific type of quantum computer, using *quantum annealing*, is already in commercial use.

Biological computing uses genes to create a biological representation of logic gates. Even though a single operation can take 48 hours, this can be done billions of times simultaneously in a single test tube.

Evolution and evolutionary algorithms solve problems by making random changes to the best adapted members of each generation. The better communication the system has, the faster these adaptations can spread through the population. This is also true of memetics, where evolution is applied to ideas.

Cloud computing uses massively parallel 'clouds' of computers to power the AI that companies like Google run on.

Evolution of species and algorithms doesn't necessarily discover globally optimal solutions, it can only approach local maxima. It can be thought of as an anytime algorithm, because wherever it is stopped it will have produced a system that is adapted to its environment, and the longer it runs the better these adaptations will be.

A genetic algorithm follows very similar rules to those of natural selection, where the programs that complete their task best by some measure are used as the next generation, and crossover is achieved by choosing some of the variable settings from two or more parents.

The problems with this are that a program first needs to be created that goes some way to solving the problem. An evolutionary algorithm can't start from scratch. It also requires the objective function to be defined, which is a non-trivial problem.

Databases are groups of tables used to store data. They provide security and concurrency, and if the database is properly normalised, then they take up as little space as possible.

Before databases were used, data was stored in files. This can be made efficient if done properly, but if the software for reading the files is lost then the data may be meaningless without it. They could also be hardware dependent.

This storage method was superseded by tables, where a row was an entity and a column was an attribute. This allows each columns to have a name and type, allowing the data to be more easily understood without the program. However, in a table, a lot of the data is redundant because it is recorded twice or more. This is a waste of space. Some fields need to be arbitrarily large, because we don't know how much data needs to go in them. This makes computations more complex.

Relational databases solve all of these problems using *normal forms*. Each table has an index called the primary key, and each entity has a unique identifier which is used as a key when searching for that entity. Any cell has at most one atomic value in it (*first normal form*). All the data in each row should depend only on that row's index (*second normal form*).

To get all the information about an entity out of a relational database, you need to join the tables. Each table must make a reference to another table's index. This is called a secondary or foreign key.

*Structured Query Language*, SQL, is used to get data out of a database or change it.
- SELECT gets one or more rows  
- INSERT adds a row  
- DELETE deletes a row
- UPDATE changes a row
- CREATE makes a new table
- DROP deletes a table

Databases not only store data, but also provide functionality through stored procedures. They also act like servers in that clients which access them can run on any platform and be written in any language.

There are risks with using databases, however.
- Crackers can sabotage the data or steal it. This can be prevented with backups, honest staff, secure and up-to-date software, logging and testing.
- The database or any part of the stack can fail. This can be prevented by using a reliable stack and having redundancy in components and systems.
- The laws regarding data storage can change. This can be dealt with by monitoring legislation and joining associations.
- The company can outgrow its data storage systems. This can be prevented by proper handling of concurrent requests and easily scalable design.

If confidential data is exposed, the company will face fines and lose customer trust. Data such as medical records, payment details and passwords should be stored on a server that isn't completely web-accessible. Users should be required to authenticate themselves with a properly encrypted password, and only able to connect over a secure connection. The database server should be in a physically secure location.

Data modification can be hard to detect if only small changes are made. This can be prevented with proper security and authentication, and monitoring of changes.

Denial of service attacks are hard to defend against, but their effects can be limited by redundant servers and specialised services.

Repudiation is where one party to a transaction denies having taken part. This can be preveted with the use of password-based authentication and digital certification.

Software errors can also pose a threat, if the software specification was wrong, the developers made false assumptions or there was inadequate testing. This can be prevented with user involvement in development and contingency plans.

The types of data storage are volatile storage, non-volatile storage and stable storage. Data is stored in a hierarchy of how often it will need to be accessed.

*Volatile* storage needs power to retain its data. If power is cut, the data is lost. Memory is volatile storage. In the hierarchy, this is primary storage.

*Non-volatile* storage can survive power outages, but is slower to access. Magnetic disks are non-volatile storage. This is secondary storage or *online storage*. Other non-volatile storage media, such as magnetic tapes and optical storage, are *tertiary storage* or *offline storage*. These have the slowest access times.

*Stable* storage is a theoretical medium that survives all failures. It can be approximated using multiple copies of the data in different locations on different non-volatile storage media.

The storage hierarchy  
![](http://i.gyazo.com/6be7f6584cefa18b88fc70b2201b38a3.png)

Magnetic disks are the primary medium for long-term storage of data. They are slower to access than memory, but are cheaper and non-volatile. The data on them can still be destroyed by disk failure, but this is relatively rare. Data is recorded by polarising magnetic cells on a spinning platter to face in one of two directions using a read-write head.

Chunks of memory are called *blocks*, and when you change something in one you need to make copies. This can result in successful completion, partial failure (destination block has incorrect information), or total failure (destination block was never updated). Keeping the data safe requires detecting and correcting these failures. There are two types of blocks - *physical blocks* are blocks residing on the disk. *Buffer blocks* are blocks residing temporarily in main memory. There are two operations to move blocks between disk and main memory:

- *input(B)* transfers the physical block B to main memory
- *output(B)* transfers the buffer block B to the disk, and replaces the appropriate physical block there.

A *transaction* is a unit of program execution that accesses and possibly updates various data items. Each transaction has its own private work area in which local copies of all data items accessed and updated by it are kept. It transfers data items between system buffer blocks and its private work-area. To start, a transaction must have a consistent database. During the transaction execution the database may become inconsistent, but a transaction isnt committed (done) until the database is consistent.
Transactions perform *read(X)* while accessing X for thie first time; all subsequent accesses are to the local copy. After the last access, the transaction executes *write(X)*. Output(Bx) doesn not necessarily immediately follow write(X), the system can perform the output operation whenever it deems fit. But until Bx is updated on the disk, it's not safe, so the transaction isnt committed. Here is a diagram showing a standard data access:

![](http://i.gyazo.com/5b6961fb513509e2f4b0c717a5370fea.png)

There are two main issues to deal with, failures (e.g. hardware failures and system crashes) and concurrency (e.g. simultaneous execution of multiple transactions. To ensure data is really saved on non-volatile memory before committment, a description of the modifications is output to stable storage without modifying the database itself. Only then is the database updated. There are two ways to do this, *shadow-paging* and *log-based recovery*.

Shadow paging assumes only one transaction is active at a time. The db_pointer always points to the current consistent copy of the database. Updates are made on a copy of the database, which the pointer moves to after the transaction reaches partial commit and pages written. On transaction failer, the old consistent copy pointed to by db_pointer is used, and the shadow copy is deleted. This assumes disks don't fail, and while useful for text editors, is extremely inefficient for a large database - executing a single transaction requires copying the entire database.

Log-based recovery keeps a *log* on stable storage. A log is a sequence of log records, which record the update activities on the database. When transaction Ti starts, it  registers itself by writing a *<Ti start>* log record. Before Ti executes write(X), a log record <Ti, X, V1, V2> is written, where V1 is the value of X before the write and V2 the value to be written to X. When Ti finishes its last statement, the log record <Ti commit> is written. This is when the transaction Ti is committed. Log records must be written directly to stable storage (they can't be buffered).

*Deferred database modification* records all modifications to the log, but defers all writes to after a partial commitment.
A transaction starts by writing a <Ti start> record to the log. A write(X) operation results in a log record <Ti, X, V> being written, where V is the new value for X (the old value is not needed for this). The real write is not performed on X at this time, but is deferred. When Ti partially commits, <Ti commit> is written to the log. Finally, the log records are used to actually execute the previously deferred writes.

During recovery, a transaction needs to be redone if and only if both <Ti start> and <Ti commit> are in the log. Redoing a transaction Ti (redo Ti) sets thevalue of all data items updated by the transaction to the new values. Crashes can occur while the transaction is executing the original updates, or while recovery action is being taken.
