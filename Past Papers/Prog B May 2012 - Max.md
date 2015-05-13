1: Lisp so not needed

2: False - An algorithm is something which can run on a turing complete machine, so should run on any OS. However a program may have platform dependencies.

3: False - The number of nodes would be the same and would therefore take the same time to search through them all. It would change the order in which the nodes are searched however.

4: False - The hashing function, i.e. converting the keys into indices in the array (for example mod 15) is a constant time algorithm. Searching the hash using linear probing however is exponential with respect to how full the array is.

5: False - The different exceptions in java are their own classes, and when an exception is thrown an object of that class is created, and passed to the catch statement if there is one for that object.

6: True - In Java, multiple threads can be prevented from operating on the same data simultaneously using the word 'sychronized' in the method declaration. This will block any threads trying to access the method if it is already being accessed by another thread. 

7: False - Only the blocks of code which need to be synchronised should be, otherwise the programmer is preventing threads from operating simultaneously for no real reason. The extreme version of this is making the whole program synchronised, in which case there is no point in using multiple threads.

8: False - Scroll bars are implemented in many languages, not just java. Nobody owns a patent on scroll bars.

9: False - Behaviour is the interaction between an intelligent agent and it's environment - it must have some effect on the environment it's in. Intelligence is the ability to generate behaviour in response to it's environment.

10: True - Breadth first search looks across every branch at one depth, and if it doesn't find a solution it looks one noded deeper and repeats. When breadth first finds a solution, it is gauranteed to be the best answer in the tree. However, this would require a lot of time and memory if there are lots of possible actions e.g. chess.

11: False - Most divide and conquer algorithms are O(n log n), for example quick sort and merge sort. Algorithms like bubble sort and selection sort are O(n^2), and are not divide and conquer.

12: 

13: True - A thread that is sleeping can be woken by any other thread in the same program with the notify() method.

14: False - The view describes not just the display on the screen e.g. widgets, but the way in which the program is presented to the user - this could be done using visual displays, sound etc.

15: True - When two threads edit the same data simultaneously, the data structure may only register one of these changes, meaning the two threads now have different views of what the data actually is. Synchronising this data forces the threads to edit the data one at a time, allowing it to be updated properly.

16: True - Listeners are used to execute a certain block of code when a particular event occurs. They are assigned to widgets such as buttons which then 'listen' for the particular event e.g. button pressed.

17: True - Productions are preconditions related to a certain action, and can therefore be either true or false, making them essentially just conditionals. They are used in Production Rule Systems in AI, in which the system goes through it's list of productions, and executes the relevant action for the one which is true.

18: True - It is impossible to assure that you will always have access to the data, because no matter how many backups are created these can always be destroyed.

19: False - AWT was used to create programs with the look and feel of the operating sytem by using native code from the OS. However, this made programs created with it unportable between OS's. Swing on the other hand is both portable and can match the look and feel of the operating system.

20: False - The fact that human intelligence hasn't been created using AI doesn't mean that AI has failed - lots of research is still occuring in the field and new discoveries and advancements are being made. It is still unknown whether or not it is possible to recreate human intelligence using AI, so it is wrong to say that human intelligence being more than ordinary computation is true or false, and it is wrong to say that AI has failed.
