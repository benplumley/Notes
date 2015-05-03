#CM10195 - Systems Architecture
##Dr Russel Bradford

An operating system is a program (often called the kernel) which:
- Manages the resources of the computer e.g. CPU, memory, keyboard, and any software that controls it.
- Provides the programmer with a usable programming interface to access those resources
The interface that the end user interacts with is just another program that uses the OS, *not* a part of the OS.

#####Managing Resources

There are 3 main reasons for managing resources:
- They are limited - There is not always enough resources to go round, e.g. mobile phones have strict limtations on memory,
CPU power and energy consumption.
- They need protection - This includes security (preventing programs from corrupting data or other programs), authorisation (ensuring that certain resources are only available to certain programs), authentication (ensuring that a program has the authorisation it claims to have), and protecting the user from their own mistakes (e.g. accidentally deleting files).
- They need to meet certain criteria - This includes responsiveness (the program needs to respond quickly, or process network packets as they arrive), real time (certain events *must* be dealt with in a fixed amount of time e.g. video streaming), security (prevention of accidental or malicious access or modification.

#####Programming Interface

The programmer who was to write applications for the machine does not want to have to know the details of the hardware, and they dont want to have to re-implement everything in every program, so the OS does this for them. Having an expert do this and provide a standard interface is a lot more practical. It means:
- The programmer doesn't have to do it, therefore saving time.
- The expert presumably has more programming experience, understands the hardware well, and is familiar with the intricacies of OS programming.

The different layers are often confused with eachother. People often confuse the GUI and some applications as part of the OS - this is largely due to marketers advertising their operating systems based on the GUI. However this is a misconception, for example embedded systems massively outsell PCs and most of these do not have even the most basic of user interfaces.

Here are two examples of layer abstraction, one good and one bad.

Good:   
![alt-text](http://i.gyazo.com/ee70ee4899e5a1dcf225f8c5e37fbb72.png)

Bad:  
![alt-text](http://i.gyazo.com/598248022cb159db1a309ec5f1f9e0f6.png)