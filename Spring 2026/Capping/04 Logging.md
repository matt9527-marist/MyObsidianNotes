**What is Logging?**
- Take things that have occurred in a program and make a persistant copy of it to be checked at a later time. 

> Logging is the writing of program state information to some sort of store
- File
- Database 
- Allocated memory 
- Program events 
- Program status
- Errors 
- Warnings 
- End-user interactions 
Etc... 

**Why do we log?**
● Logging is used to record what occurred in  
our program  
● Without a log, it can be difficult or  
impossible to understand problems  
● A good log can make debugging customer  
issues much easier

Without knowing what happened, we cannot debug or audit our systems. 

![[Pasted image 20260203175840.png]]
Linux has *syslog*, which lists all daemons (services) can write to. 
Mostly used for debugging or problem analysis. 
Windows has the system Event Viewer. 

**Using Syslog**
● It's very simple to use  
	– Use “logger” shell command  
	– Use syslog() C API  
● Messages have an origin and a priority (can measure importance of issue)  
	- Only show errors vs. show everything 
● Administrator can filter based on priority level  
	– Might only want to see severe errors  
	– Ignore informational messages to cut down on  
	traffic

**What happens if we do not log?**
● Don't know why programs crash  
	– No stacktrace  
● Don't know when daemons start or stop  
	– No syslog  
● Don't know the internal state of our programs  
	– No program logs  
● Makes performing service much more difficult!

**What happens if we do not log *enough*?**
● Imagine that our application is running.  
	– It crashes for some reason, and provides a stack  
	trace  
	– We have logs showing that it started and ran  
	successfully  
● What if the stack trace is ambiguous?  
● What if there are many ways that particular code  
can be reached?  
● How did the crash occur?

We usually hope to crash really close to the logs. 

● Imagine that our application is running.  
	– It crashes for some reason, and provides a stack trace  
	– We have logs showing that it started and ran  
	successfully  
● What if the stack trace is ambiguous?  
● What if there are many ways that particular code can  
be reached?  
● How did the crash occur?  
*● Might need to reproduce the problem!*
We must be proactive and capture the logging data before a failure occurs. What happens when the program crashes? If we can see when a crash happened, we should be able to see what was happening around it. We must design this in from the start. 

**First Failure Data Capture**
● The idea that a program will log enough  
information that when it fails, it can be  
successfully debugged and serviced  
● Asking customers to reproduce a failure in  
a complex environment on a production  
system is unacceptable!  
● This level of detail should be designed into  
the system from the start

**Goal**
Ensure that your application logs  
appropriately  
● Make sure traces and dumps are captured  
● Log start and stop events  
● Log internal problems for analysis  
● Log internal events for informational  
purposes

