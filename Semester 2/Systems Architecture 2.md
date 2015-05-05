#CM10195 - Systems Architecture
##Dr Russel Bradford

An operating system is a program (often called the kernel) which:
- Manages the resources of the computer e.g. CPU, memory, keyboard, and any software that controls it.
- Provides the programmer with a usable programming interface to access those resources
The interface that the end user interacts with is just another program that uses the OS, *not* a part of the OS.

####Managing Resources

There are 3 main reasons for managing resources:
- They are limited - There is not always enough resources to go round, e.g. mobile phones have strict limtations on memory,
CPU power and energy consumption.
- They need protection - This includes security (preventing programs from corrupting data or other programs), authorisation (ensuring that certain resources are only available to certain programs), authentication (ensuring that a program has the authorisation it claims to have), and protecting the user from their own mistakes (e.g. accidentally deleting files).
- They need to meet certain criteria - This includes responsiveness (the program needs to respond quickly, or process network packets as they arrive), real time (certain events *must* be dealt with in a fixed amount of time e.g. video streaming), security (prevention of accidental or malicious access or modification.

####Programming Interface

The programmer who was to write applications for the machine does not want to have to know the details of the hardware, and they dont want to have to re-implement everything in every program, so the OS does this for them. Having an expert do this and provide a standard interface is a lot more practical. It means:
- The programmer doesn't have to do it, therefore saving time.
- The expert presumably has more programming experience, understands the hardware well, and is familiar with the intricacies of OS programming.

The different layers are often confused with eachother. People often confuse the GUI and some applications as part of the OS - this is largely due to marketers advertising their operating systems based on the GUI. However this is a misconception, for example embedded systems massively outsell PCs and most of these do not have even the most basic of user interfaces.

Here are two examples of layer abstraction, one good and one bad.

Good:   
![alt-text](http://i.gyazo.com/ee70ee4899e5a1dcf225f8c5e37fbb72.png)

Bad:  
![alt-text](http://i.gyazo.com/598248022cb159db1a309ec5f1f9e0f6.png)

An OS should be efficient and lightweight: every CPU cycle that the OS uses is one that is taken awaay from the user's programs. It should also be flexible and not get in the way of the programmer - so a perfect OS would be completely invisible.

####Background

An OS is just a program, so we can have differents OSs on the same hardware, and the same OS on different hardware, e.g. on intel hardware (PC) you can run Windows, OS X, Linux and many others. Since an OS has to deal with the details of hardware, it is not entirely trivial to port on OS from one architecture to another. Well designed OSs mninimise the hardware dependent parts and try to keep mose code hardware-independent. Historically, some OSs tied themselves too closely to the hardware so that porting was very difficult. For example, for much of its lifetime Windows only ran on Intel, so the assumption of Intel hardware ran throughout the code. In contrast, the Android OS shares a large amount of code with the Linux that runs everywhere else.

The general public often think of the OS as the GUI (there is some basis for this confusion, as Microsoft and Apple tie their GUIs indivisibly to their OSs), and some software companies encourage and make capital out of this confusion.

####History

At first, computers had no operationg systems (1960s) - every programmer had to write their programs for the particular machine they were using, and therefore had to know exactly what kind of hardware they had and how to use it. This meant there was no portability, and lots of repeated code between programs.

In fact, programmers rarely even saw the computer. The program and the data (collectively called a job) would be prepared on paper tape or punched card. Jobs would be given to operators who would load and run them, then give the results back. Usually there would be a bug and the programmer would have to fix the program and go round the loop again. Computer time was limited, so scheduling the jobs for the computer was done by hand. Turnaround on these jobs could be days.

