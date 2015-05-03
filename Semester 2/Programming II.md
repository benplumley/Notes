#CM10228 - Programming
##Dr Joanna Bryson

All programming languages run on physical computers, take time to run, take space in memory, and run algorithms. The amount of time and space a program takes to run is known as the program's *complexity*. Algorithms with lower complexity are better.

The *Church-Turing thesis* says that any algorithm can be run on a Turing machine. All computers are Turing equivalent, and every real programming language is Turing complete. An algorithm is defined as something that can run on a Turing machine.

Languages can be *compiled* or *interpreted*. Compiled code is turned from human-readable code to machine code long before being run, interpreted code is evaluated line by line. Compiling means the program will run faster, but the compiled code will be less transportable between different computer architectures.

Languages can be *strictly typed* or not. A strictly typed language defines the data type of a variable when that variable is created, and only allows objects of that data type to be assigned to that variable. Non strictly typed languages do not associate data types with variables; the data type of the variable is simply the data type of the object currently assigned to that variable.

Languages can be *object oriented* or not. An object oriented language allows any piece of code and data to be defined as an object that can be instantiated and passed around.

Languages can be *high* or *low level*. A high level language is closer to being human-readable, and tends to be more verbose. A low level language is closer to being understood by a computer, and tends to be more compact.

Languages can be *dynamic* or not. A dynamic langauge can write and evaluate (run) new code whilst currently running. For instance, a program could contain a text box accepting code in the language it is running in that would then run as part of that program.

In the real world, not all languages fit these binary definitions. Java, for instance, is partially compiled and partially interpreted, strictly typed, object oriented, high level, and partially dynamic.

Arrays of primitive data types are chunks of adjecent memory locations. Arrays of objects are arrays of references to other memory locations containing the objects in the array. An item in a list is made up of two references, one to the object at that position and one to the location of the next item in the list. The "next" reference of the last list item is null.

Arrays are faster when the array length is known ahead of time. This is because accessing the nth item in an array is a constant complexity operation; it takes as long to find the object at position 100 than the object at position 1.

Lists are faster when the length isn't known or is likely to change. To change the size of an array, a new block of memory the right size must be found and the old data must be copied into it. To change the size of a list, the pointer of the last item must be changed to that of the new last item. However, accessing the item at position n in a list is a linear time operation; accessing the object at position 100 might take 100 times longer than accessing the item at position 1.

Lists also make it easier to add a new item into the middle - in an array, the last half of the array would have to be moved and the new item inserted into the space. In a list, only the item immediately before the one being added must have its pointer changed to point at the new item, then the new item can carry on the list by pointing to the next one.

In modern computers, the time taken to complete these operations is negligible in most cases.

The language *Lisp* implements lists as described here. The reference to the object is called *first* and the pointer to the next list item is called *rest*.

Sorting is useful because it makes searching faster. A sorted list can be searched with a binary search in logarithmic time, an unsorted list must be searched item by item in linear time. It is therefore useful to common applications of searching to sort the list first.

Artificial intelligence can be generalised to a problem of searching a list of things to do for the best one, and this must be performed quickly otherwise the conditions specifying what a good thing to do is may have changed by the time an action is chosen.

Items in a list are sorted using a key. This is a piece of the data that is part of the list item. For instance, the key to sort a dictionary is the word to be defined. The key to sort a phone book is the name of the person. Choosing the key is sometimes non-trivial; it should (or must) be unique, have a sensible order (eg numerical, alphabetical, chronological) and be the part of the object that is already known. A phone book ordered numerically by phone number would be useless.

*Selection sort* can use two arrays. The first array is iterated through to find the smallest item, which is inserted into the first position of the second array. This is repeated until no items are left in the first array. The second array is sorted.

Alternatively, this can be done with a single array, instead of putting the smallest item into the first position, the smallest item and first item are swapped. This requires an extra temporary variable for storing the value of the item being swapped.

**Selection sort is O(n^2).**

*Insertion sort* splits the array into sorted and unsorted parts. Initially, the sorted part contains only the first item of the whole array. Then the first item of the unsorted part is inserted into the correct position into the sorted part and removed from the unsorted part. This is repeated until the unsorted part has no elements.

**Insertion sort is O(n^2).**

*Quick sort* chooses a number (typically the one in the middle of the array) as the pivot. All numbers smaller than this pivot are put into a new array to the left of the pivot, and likewise with larger numbers to the right. This is then repeated recursively on the new smaller arrays. When all arrays contain a single element, putting these back into a single array in the order they are currently in will result in an ordered list.

**Quick sort is O(n log n).**

*Bubble sort* starts at the first element, compares it to the second, and swaps them if they are out of order. It then repeats this from the second. Once it reaches the end, it comes back to the second item and repeats the process.

**Bubble sort is O(n^2).**

*Merge sort* splits the array in half recursively until each array has only one element. These arrays are then merged two at a time, sorting the items into the correct order at each merge.

**Merge sort is O(n log n).**

Algorithms which solve their problem by splitting the input in half recursively, such as quick sort and merge sort, are known as *divide and conquer* algorithms.

Algorithms are evaluated based on their speed, size, risk of failure and ease of maintenance. The complexity of an algorithm typically is referring to its speed, but could also mean size. Due to the speed of modern computers, a slower but easier to maintain might be preferable because the computer's time is cheap compared to that of a programmer to maintain it. However, in situations where the result is needed quickly such as when rendering in a game engine, the speed of the algorithm is more important.

Speed of an algorithm is measured by counting the number of basic operations the algorithm performs. More importantly, the complexity is a measure of how this number of basic operations changes as the amount of input data the algorithm is processing changes. This is known as the *scaling* of the algorithm. This scaling happens with respect to some independent parameter. For a sorting algorithm, this parameter is the number of items to be sorted.

An algorithm is called *fast* if it grows quickly, so a *slow* algorithm is better. In order from slow to fast, algorithms can be constant, logarithmic, linear, quadratic, polynomial, exponential, or factorial.

A *binary tree* is like a list, except rather than each item having one pointer to an object and one pointer to the next item, has one to an object, one to the child "right" of it and one to the child "left" of it. Finding an item in a binary tree is log 2 complexity.

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

Simplistically, programs execute sequentially from the first statement to the last. The program counter keeps track of the current line number. *Non-linear flow of control* is the deviation from this sequential flow introduced by statements such as goto and loops. In Java, *break* and *continue* are used in loops to change the flow of control. Break jumps out of the current innermost loop, or to the label if one is used. Continue skips all the remaining code in the current loop and goes back to the start of the next iteration.

When a process dies or is killed, it is unsafe to simply stop its threads from running. To exit cleanly, a program must close any files it has open and give up any other resources, and kill any children it spawned. It will probably want to save its state to disk.

When something goes wrong in many programming languages, the program is said to throw an exception. The routine for dealing with this problem occurring is said to catch the exception.

In Java, *throwables* are errors and exceptions. They are full objects which can be instantiated and passed around. An *error* is something that can't be solved by the program whilst running, such as syntax errors. An *exception* are things that the program may be able to solve whilst running.

Exceptions are further split into *checked* and *unchecked*. Checked exceptions must be caught and dealt with in order to compile. For instance, lots of IO operations can't be called without catching their possible IOExceptions. Unchecked exceptions mean the programmer has made a mistake. These don't have to be caught, but can be.

Checked exceptions must be put inside a try clause, followed by a catch clause containing code for handling that particular exception. Finally clauses run after all other clauses.

Throwing a checked exception can be done by creating a new Throwable and using the throw keyword. Methods which throw exceptions and don't catch them must instead *propagate* them, or pass them up to the calling method. A method's ability to do this must be included in the method signature.

Throwing and propagating unchecked exceptions is done automatically and implicitly.

>8
