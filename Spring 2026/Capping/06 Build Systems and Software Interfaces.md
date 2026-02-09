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

