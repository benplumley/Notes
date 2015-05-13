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

10. True. 
