**Building Software**
● Transforming source code into executable code  
● Can be done on an ad-hoc basis via command-line  
statements  
	– Tends to be error-prone  
	– Leaves room for mistakes  
	– Easy to mess up command syntax with a stray character  
● Scripted build systems are better  
	– Reduces human involvement  
	– Can capture knowledge in the tool

**Build Scripts**
● Just a sequence of compiler commands  
● Can be a bash script or batch file  
● Very simple, to implement  
● Doesn't add much benefit to the process  
● Requires manual updating for almost any  
change

**Makefiles**
● Very old – part of original UNIX  
● Pretty simple to write  
	– Implementation is relatively straightforward  
● Just a list of directives with commands  
● Can create manual dependencies  
● Uses file timestamps to determine if a  
rebuild is necessary
Example: 
![[Pasted image 20260209182758.png]]

**Autotools**
Designed by the GNU Project  
● Used to configure and build  
many open source components  
● Mainly used for C programs  
● Easy to run  
	– ./configure && make && make install  
● Horrendously complex to write!  
	– Hundreds and hundreds of tests are run on a system, probing for  
	capabilities  
	– Need to account for differences for each system in project source  
	code

**Scons**
● Python based build tool  
● Automatic dependency generation  
● Built in support for many major languages  
● Similar functionality to GNU  
autoconf/automake
Example:
![[Pasted image 20260209183007.png]]

**CMake**
● Two stage building  
– Generates build files, then native build tools  
are used for compiling  
● Can build outside source tree, unlike  
Makefiles

**Apache Maven**
● Maven means "accumulator of knowledge" in Yiddish (מבין)  
● Uses convention over customization  
	– Only exceptions to defaults need to be documented  
	– Don't need to specify compiler flags unless different  
● Driven by XML files (pom.xml)  
● Has a plug-ins for extensibility  
● Mainly designed for Java development  
	– Very easy to deploy jars and such  
● Can be used for C and native code with some fiddling  
● Can build outside source tree, into “target” directory
*Minimal Maven POM*
![[Pasted image 20260209183103.png]]

**No Assembly Required**
● Some languages don’t require a manual  
compile step  
	– Python is automatically compiled the first  
	time a source file is run  
	– It produces `*.pyc` files that are architecture  
	and OS dependent  
	– These can be distributed along with source  
	code if desired

**DevOps and Automation**
● Continuous integration / continuous delivery  
	– Building code is done automatically upon check-in  
	– This is performed via an automation server  
		● Jenkins, Travis, UrbanCode  
		● Build scripts are written ahead of time, and run as part of a  
		build job  
	– Build errors are caught early on, improving software  
	quality  
	– Can be used to run a test suite after successful build

**For Our Project**
Use a build system for your project  
● It must be repeatable and documented  
● It must be stored with your source code  
● It's better to use a more modern build system  
than an ad-hoc script  
● Use a build system that meshes with your  
choice of language  
	– Java → Ant/Maven

## Software Interfaces 
**Interface Types**
● Interfaces have a variety of audiences  
● Human  
	– Command-line & GUI  
● Other software  
	– Application Programming Interface (API)  
● Hardware  
	– Registers, memory maps, and interrupts

**Introduction**
What is an interface?  
	– A way of interacting with a piece of hardware  
	or software  
● An interface provides access to computer  
resources  
	– This can be hardware or other software

**Human Interfaces**
Designed for interactive use  
● Should be “intuitive” and easy to use  
	– That’s a loaded statement!  
	– What’s easy for some users is maddening to  
	others  
● Need to consider use case of software and  
intended audience  
	– Newbies / Power Users / Developers

**Computer User Skill Distribution**
> Across 33 rich countries, only  
   5% of the population has high computer-  
   related abilities, and only a third of people  
   can complete medium-complexity tasks.

**Command Line**
Early form of interface  
● Easy to implement (POSIX  
getopt)  
● Good for experienced users  
	– Keyboarding is always faster than  
	mouse  
● Easily automatable via scripts  
● Can look scary to newbies  
● Complex software can have a  
dizzying array of options  
	– /bin/ls has 60 different arguments!

**Full-screen text-mode Interface**
● Does not require graphics hardware  
	– MS-DOS editor, Linux, IBM 3270  
● Can be line-based or screen-based  
● Need libraries to control terminal behavior  
	– Not simple to implement  
	– curses / ncurses
![[Pasted image 20260209185045.png]]

**Graphical Interfaces**
● Presentation logic is separate from  
application logic  
	– Makes it easier to change interface without  
	changing how application works  
	– Can move widgets around easily for rapid  
	prototyping  
● Easy for users to explore...sometimes!
● Originally developed by XEROX  
● XEROX Alto had the first mouse-driven interface
Apple borrowed heavily from it for the  
Macintosh user interface
- Decoupling the interface with the underlying native code is a good thing because we can then change trhe

**Bulk Rename Utility**
![[Pasted image 20260209185108.png]]

**Windows**
![[Pasted image 20260209185159.png]]
● After numerous iterations, the interface  
design (mostly) stabilized

**Linux**
● Huge variety of window managers  
● Graphical interface is separate from the  
rendering subsystem (X11)
![[Pasted image 20260209185237.png]]

**Application Programming Interfaces**
● APIs are used for connecting software together  
	– Provide a documented way for communication  
	between software  
	– Sometimes dictated by a standard (POSIX, C11)  
● APIs define some of the following  
	– Method signatures  
	– Data types  
	– Return values  
	– Error conditions

It’s important to get API design right  
● Unlike a GUI, it’s expensive and disruptive  
to change an API  
● Other software depends on it  
● Sometimes you can’t change it, and just  
introduce a new API  
	– This leads to interface sprawl!

**Hardware Interfaces**
● Used to communicate between hardware components  
● Also between hardware and software  
● Very expensive to change  
	– Can require rolling out new silicon!  
● Memory-mapped I/O  
	– Read and write to specific memory addresses  
● CPU Registers  
	– Function calling conventions

**Sequential Sunburst - For our Project**
![[Pasted image 20260209185435.png]]
