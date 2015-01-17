#CM10227 - Programming
##Dr Rachid Hourizi

**Syntax Errors** are errors in the program to do with how it is written. They are found by the compiler, and the program can't compile until they are fixed.

**Runtime Errors** are errors that occur during the running of the program by uncaught exceptions. Code robustness is the ability to deal with unexpected exceptions without crashing.

**Logic Errors** are mistakes made by the programmer that do not cause the program to crash, but give an output that is not what the programmer wanted.

**Debugging** is the process of finding and removing bugs from a program.

**Low level languages** like assembly language are close to what is directly executed on the computer. Programs written in them are fast and use little memory.

**High level languages** like Java are more abstracted from what runs on the computer, but much easier to read, write and debug. They can also be compiled to run on many different processors.

**Interpreters** convert high level code into machine code via assembly language one line at a time, and then immediately perform that line. The process of interpreting is fast, but an interpreted program is slow.

**Compilers** turn a whole program from high level code into machine code in one step. Compiling a program takes time, but the program runs quickly once compiled. Java is compiled to JVM bytecode, which is not machine specific (or rather, it runs on the Java Virtual Machine, which can be installed on any machine). The bytecode is then interpreted.

**Variable declaration** is the process of assigning memory to a variable.

**Variable instantiation** is the process of assigning a value to a variable for the first time.

**Garbage collection** is the automated deletion of variables (and freeing of their memory) as soon as they are out of scope.

**Parameters** appear in the definition of a method to specify what the method needs to be provided with when it is called.

**Arguments** are the objects passed into a method to satisfy its parameters.

**Statically typed** languages force the type of each variable to be defined at compile time and then can't be changed.

**Dynamically typed** languages don't require a data type to be stated, and instead change depending on what value is assigned to them.

**Strongly typed** languages don't allow implicit conversion of variables. For instance, the need for the parseInt method makes Java strongly typed:  
	int i = 5;  
	String s = "8";  
	i = i + Integer.parseInt(s);  

**Weakly typed** languages convert variables implicitly depending on the operation being performed on them. For instance, in a weakly typed language, the following pseudocode is valid, resulting in i=13:  
	int i = 5;  
	String s = "8";  
	i = i + s;  

**Type coersion** is the implicit conversion of primitives, for instance when dividing an integer by a float, the integer is implicitly converted to a float before the division even in strongly typed languages.

**Code robustness** is the ability to gracefully warn the user or exit without crashing when an error occurs.

**Scope** of a variable is the block of code that is aware of the variable's existence. For instance, the scope of a global variable is the whole class, and the scope of a variable defined in a method is that method.

**Recursion** is the process of a method calling itself, each time pushing the current stack frame to the stack.

**Stack** is an area of memory used for storing stack frames from method calls, and global variables. Also a data type where elements enter and leave from one end.

**Incremental development** is a method of programming where functions are added and fixed one at a time, so the program is working for as much time as possible, rather than adding a lot of new functions then debugging them all.

**Encapsulation** is putting code that does one particular task inside a method or class, so that its implementation can be changed without changing how it is used from outside. It also prevents the user from accessing data about the implementation.

**Generalisation** is making code that solves a specific problem into code that solves a general problem.

**Immutable data types** can't have their values modified after creation. To change the value of a variable with immutable type, a new memory location is used and the variable is updated to point to the new location.

**Mutable data types** can have their values modified after creation. The memory location storing their value is overwritten with the new value when it is changed.

**Abstract data types** are classes whose implementation is encapsulated.

**Queue** is a data type where elements leave at the opposite end to where they joined.

**Class** is a template for an abstract data type. Classes are provided by Java and we can also write our own.

**Object** is an instance of a class.
