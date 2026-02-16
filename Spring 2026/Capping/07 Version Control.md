**What is Version Control?**
>“A class of systems responsible for managing  
   changes to computer programs, documents, large  
   web sites, or other collections of information”[1]  

● Using source code control, or version control, is a  
critical part of modern software engineering  
● It allows a team to work together in a cohesive  
manner on a complex software product  
● There is no excuse for not using it on any software  
product – period

**Local Version Control**
● Only works on a single system  
● Uses a special directory to store file metadata  
● Designed to work on a shared server with multiple  
developers  
● Each user requires a shell account on the server  
● Offline development isn’t really possible  
● Server is a single point of failure  
● Examples: SCCS, RCS
- Single point of failure, not as much of a problem in the 1970s.

**Client-Server Version Control**
● A single source code server works with multiple clients  
● Each developer checks out source tree to their local workstation  
● Changes are made, and checked in back to the central server  
● Offline development is possible, but checkins require network access  
● Server is a single point of failure  
● Handling changes from other developers without repo access is  
clunky  
	– Emailing compressed patch files was a common workflow  
	– This pain point caused Linus Torvalds to create Git  
● Examples: CVS, Subversion

