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

*Insertion sort* >2.4.1
