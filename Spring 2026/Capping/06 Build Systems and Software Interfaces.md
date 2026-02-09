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

