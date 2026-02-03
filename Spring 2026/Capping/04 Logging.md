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

