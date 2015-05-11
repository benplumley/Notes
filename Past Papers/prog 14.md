1. False. Although every Turing-complete language is technically capable of implementing any algorithm, different languages are designed to be better at different tasks. By choosing a more suitable language, the program can be more efficient, easier to write, and easier to understand.

2. False. If the data happens to be in the best case for Bubble sort, it will take O(n) time, where Merge sort will still take O(n log n) time. In this case, Bubble sort will be faster.

3. False. In a hash (as opposed to a hash table), looking up an index of an item that does not exist is constant time, the same as looking up the index of an item that does exist.

4. False. Although a hash search has a lower complexity than a binary search, in practice as the question specifies there may be overheads associated with the hash search that are discarded by formal analysis but counted by the stopwatch. These could add up to make the hash search slower, especially for small data sets.

5. False. A counterexample is a hash search, which uses pointer arithmetic to find any item in the hash in the same time, no matter the size of the hash.

6. True. In Java, Class is instantiated whenever a class is created, and can do work because it has methods for things such as getting the class of the calling object.

7. False. Although languages with while loops are still Turing-complete when GOTO is removed, some algorithms can be significantly shortened when GOTO is used. This is arguably a legitimate use of GOTO, though the main school of thought, popularised by Dijkstra, is that GOTO is harmful and should always be avoided.

	However, this does not mean it is not used in commercial code. For instance, a bug in Apple software in 2014 was found to have been caused by improper use of GOTO.

8. False. Signals can be sent between threads in the program (for instance, to wake from sleep), but the kernel can also send signals to threads in a separate program. When the user presses ^C at the terminal, a signal is sent from the kernel process to the application process, so between two different programs.

9. True. If the catch statement catches a specific checked exception and the code in the try statement throws a different and unchecked exception, this will not be caught in the catch statement but propogated to the calling method.

10. True. This works on deadlock because one of its symptoms is that deadlocked threads will be blocked waiting for one another's resources, and when they are killed the resources they held will be released. This won't work work on livelock because livelocked threads don't become blocked, they simply wake and immediately sleep, something that is not as easy to tell apart from normal behaviour.

11. False. A Java GUI application typically extends from the JFrame or JPanel class (or a child of either), which are the view. It is also incorrect to refer to any part of MVC as the 'core', because removing any one would break all functionality, meaning they are equally as important.

12. False. GUI components can track the mouse whether the button is clicked or not. This is how buttons are able to change appearance when hovered over, and programs such as first-person games are able to point the camera depending on where the mouse is moved without being clicked.

13. False. Some internet protocols are not human-readable, others are. For instance, SMTP is largely human-readable. This aids debugging and allows relatively simple clients to be created. It is possible for a human to spoof an SMTP client without the mail server knowing.

14. True. Holding a monopoly is not illegal or even inherently bad. However, Microsoft abused this position to hurt their competition, an illegal practice known as anticompetitive behaviour. Lack of competition harms society as a whole because the company holding the monopoly has no incentive to make progress in their field if there is no danger of them being overtaken by a competitor.

15. True. Patents apply to a problem, not to a solution. If a company creates a program to solve a specific problem and gets a patent, no other company can sell a program solving the same problem. Other solutions can be developed, provided they are only used in academia, and sold when the patent expires after 20 years.

16. False. Depth first search can find the best solution, but only if it searches the entire tree. In comparison, breadth first search does not have to search the entire tree to guarantee it has found the shortest solution.

17. False. Humans do plan, but not as formally as AI does. A counterexample is a chess game, where planning is more useful to a human than learning - a few good moves can be learned, but the best chess players always plan moves ahead in the same way AI does.

18. True. Evolutionary algorithms are limited in that they require a solution that solves the problem to some degree to use as the basic structure for the first generation. This solution can then be improved upon, but this relies on chance to approach anything other than the original solution's local maximum.

19. True. Assuming the database is properly normalised, each table stores only one relation. The data relating to the student's visas is unlikely to be in the same table as their identification number. Instead, the table containing the identification number will contain a secondary key which is the primary key of the table containing visa data, joining the two tables.

20. False. Robotics is not advanced enough, or advancing quickly enough, that robots will be able to do all of today's jobs within the next 5 years. Even if the timespan in the question was changed so that it was likely that all of today's jobs could be completed by robots, new jobs that don't exist today would have been created by then that can't be done by robots, exactly as happened in the industrial revolution.
