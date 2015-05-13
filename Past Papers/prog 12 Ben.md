1. False. reverse-help calls itself, therefore is a recursive algorithm. This means the sublists will also be affected.

2. False. Microsoft PCs, Linux machines and Apple Macs are all Turing complete, so the same algorithms (ie all algorithms) can run on any and all of them.

3. True. By the formal definition of complexity, a ternary tree would have O(log_3(n)) complexity, meaning it was better than a binary tree, and so on for more branches per node. However, in practice, the extra time this would take to implement and the fact that computers are so heavily optimised to make binary calculations means that binary trees are most likely the fastest implementation in practice.

4. False. However, this depends on a couple of factors. The first is what is meant by "the hashing algorithm". If this means the hash function, then this algorithm should always be constant time (which algorithm is used can be decided by the programmer, but it would be impractical to choose one that is not constant time).

	If it meant the search algorithm, then this again depends. If linear probing is used, then this is exponential with respect to the fullness of the hash. If chaining is used, it is linear with respect to the fullness of the hash.

5. False. Java throwables, including exceptions, are full objects which are created where they are thrown and this object is passed into the catch clause. Full objects are also propogated.

6. True. Synchronized blocks are typically used for concurrency in Java. However, explicit locks in the form of mutexes do exist in Java, but the traditional way of locking is through synchronisation.

7. False. The opposite is true - when using synchronized blocks, it should enclose as few lines as possible for the code to still be thread-safe. This is because blocks of synchronised code can only be run by one thread at a time, and if these blocks are large then they can easily form a bottleneck in a multithreaded application.

8. False. Scroll bars are implemented in Java, but they are also implemented in almost all other langauges that allow windows to be created, including many languages that came before Java. Nobody has a patent on scroll bars.

9. False. Behaviour is definitionally something with an effect on an environment, whether this effect was arrived at through intelligence or through traditional algorithms. Intelligence - specifically intelligent agency - is the ability to respond to external forces and adjust behaviour accordingly. What is described is a traditional deterministic algorithm.

10. True. The other potentially bigger problem for using breadth-first search in large problem spaces is the amount of working memory needed, which easily outgrows the practical and even theoretical limits of possible memory size when applied to large problems such as chess.

11. False. The hallmark of a 'divide and conquer' search is that its complexity will have a log n component. For instance, Quick sort and Merge sort are divide and conquer algorithms, and both have O(n log n) complexity. Search in a binary tree is one of the most basic examples of divide and conquer, and its complexity is O(log n).

12. True. The only difference between the parent and child processes immediately after a fork is the return value of the fork function. The program counter points to immediately after the fork and the first instructions to be executed are likely comparisons of this return value to determine whether to execute the parent code or the child code.

13. True. A thread that is asleep or waiting can be woken or notified by any thread in the same program, or by the kernel process.

14. False. A view does not necessarily refer to something that must be seen. In a properly modular  program, the visual View could easily be swapped out for an auditory or tactile view with identical functionality.

15. True. If two threads modify the same thread-unsafe data structure simultaneously, the data structure could register only one of these changes, or some corrupted combination of the two changes. This data is now inconsistent with what it should be, and what the threads believe it to be. When this structure is synchronised, the updates are forced to happen one at a time, meaning the structure can't become inconsistent.

16. False. Any Java object can be assigned a listener, but in practice they are only useful when given to widgets.

17. True. In the most simplistic implementation of a production-rule system, a single production is associated with a single action and if that production is true, that action is carried out. This could be implemented exactly as a list of conditionals.

18. True. No matter how many backups in different locations and on different media are created, there is a possibility that all can be destroyed. Stable storage can never be achieved, only approached.

19. False. AWT used native OS code and so was able to look identical to GUI programs created in a machine's native language, but this made it unportable and so defeated the point of what Java was created for. Swing is more typically attributed with Java's success, because it was portable and could match the look and feel of an operating system.

20. False. It is wrong to suggest that because a human-level AI has not been created yet, that AI has failed. AI has been created very successfully and is used to create almost all the value of some companies, such as Google.

	Whether it will be possible to create human-level AI, or whether human intelligence will turn out to have some uncomputable component, is still an open question and an area of active research. One school of thought says that the human brain does not perform only computation, but has some inherent understanding allowing for real emotion and self-awareness. This suggests that computers can never be conscious in the same way humans are.

	The opposing view is that since the human brain is constructed entirely of interacting components, at the lowest level these are simple enough to model individually. When (and if) computers are powerful enough to model as many of these as exist in the human brain, the resulting system will be functionally identical to a biological human brain, the only differences being processing speed (which is limited by the clock speed of the simulating machine rather than the speed of light and the dimensions of the brain) and the sensory inputs (hence even a perfectly simulated brain will not follow deterministically the same paths as the 'donor' brain).

	Given time, this first difference can be overcome, and the second doesn't matter because all human brains receive different sensory inputs anyway. Once this is acheived, the simulated brain will be equal in intelligence, self-awareness and consciousness as the human whose brain was modelled.
