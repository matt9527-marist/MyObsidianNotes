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

**Distributed Version Control**
● One or more version control servers work with multiple clients  
● Requires network access for initial source tree clone  
● Changes and commits can be done offline  
● Synchronizing with the repo must be done online  
● The git “server” isn’t special – each repo is functionally identical  
● Better handling of code change requests from other developers  
– “Pull requests”  
● Examples: Mercurial, Git

**Branching**
● Source code management systems support branches  
– This means that code can be split off into a separate area for work /  
experimentation  
– If/when it is complete, the branch can be merged back into the  
mainline code  
– This keeps dangerous or disruptive changes away from the main  
codebase  
– Git handles branching in an ideal manner  
	● Other SCM systems have clunkier
![[Pasted image 20260216182615.png]]

**Brief History of Version Control**
● *Source Code Control System (SCCS)*  
	– Part of AT&T UNIX distribution  
	– Created in 1972 in Bell Labs  
	– Stores each file separately, and a list of patches for each file  
● *Revision Control System (RCS)*  
	– Created in 1982 by Walter F. Tichy at Perdue University  
	– Improved on SCCS by using a reverse-delta format for  
	change history  
		● Latest version of file stored, and patches used to back up to original  
		version
● *Concurrent Versions System (CVS)*  
	– Created in 1986  
	– Acts as a front-end to RCS  
	– Adds support for repository-level changes, and  
	client-server network connectivity  
	– Server can allow for “anonymous CVS access”  
		● Anyone can check out code, but cannot commit  
		changes
● *Subversion*  
	– Created in 2000  
	– Repository changes are atomic commits  
		● CVS could corrupt the repo if interrupted  
	– File renames are handled correctly  
	– Files aren’t individually versioned – the entire repository  
	has a commit number.  
		● Making a commit increments the number  
	– Native client-server architecture for network access  
		● Clients have to be online in order to work with the repo
● *Git*  
	– Created in 2005  
		● Built as a response to the Linux kernel losing the ability to use the proprietary  
	Bitkeeper SCM system  
	– Primary design point was to easily handle distributed development  
	– Manual handling of software patch files was a major time sink for  
	Linux kernel maintainers  
		● Pull requests make dealing with patches much simpler than working with  
		email attachments  
	– Creating branches in git is essentially “free” and instantaneous  
	– Most repository actions can be done without network access

**Why Use Version Control?**
● Using version control used to be uncommon for most non-  
enterprise developers  
	– A shared drive on a server would hold the source code  
	– All developers would have write access to the raw source files  
	– This is simple to setup, but terrible for reliability or tracking changes  
	– Using version control added a layer of complexity over just editing  
	the source code  
	– A small, co-located team with a local file server was typical to how  
	development was accomplished  
	– Many cases where source code for historically important programs  
	has been lost
● It gives you a history of changes  
	– Useful for figuring out when a bug was introduced or fixed  
	– Can be helpful in a lawsuit to prove code provenance  
	– Modern SCMs guarantee code can’t be changed without a  
	commit  
	– Distributed SCMs allow for asynchronous remote development  
	– Adding new features with branches makes it easier to follow  
	along with mainline changes while not breaking the code with  
	new features  
● The rise of GitHub, GitLab, etc. has made not using source  
control more inconvenient than the alternative