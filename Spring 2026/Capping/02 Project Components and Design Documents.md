**Sample Implementation of Project**
High Level View:
● Metrics collector  
	– Java code  
● procfs  
	– Native C code  
● Syscalls  
	– JNI C -> Java translation  
	– Metrics aggregator  
● Find metrics delta over an interval  
● Database interaction  
	– Store metrics on a per-process basis  
	– Keep metrics data over time  
● User interface  
	– Report generation  
	– Present data to end user

**Metrics Collector**
● Will run periodically  
	– Exact interval left up to the team  
● Gather process metrics from various sources  
	– Procfs for memory, process elapsed time, etc  
	– sysconf for length of a kernel tick  
● Different metrics use a variety of units  
	– Need to harmonize into sane and consistent data formats  
● Some metrics are easy to collect, others are more esoteric  
● Aggregate into interval

**Database**
● Relational database is suggested  
	– SQLite is very simple and easy to implement  
	– MySQL / MariaDB are more heavyweight  
	– NoSQL (like MongoDB) could work  
● Connect with Java via JDBC API  
	– Write SQL statements to store aggregated metrics to table  
● Data amounts can decline over time  
	– Recent data has high granularity  
	– Older data will be aggregated and reduced in frequency  
	– Use reasonable thresholds – exact details are up to the team  
	– Helps to make storage requirements reasonable

**Expectations**
Projects must work on a generic OS install  
	– “It works on my machine” is unacceptable  
	– Must use “reasonable” amounts of memory and CPU  
		- It's a monitor; it shouldn't crash with little resource or take up all the resources it's trying to monitor.
● Applications should not crash or fail  
● Design documents will show how application is  
structured  
● Test documents will explain testcases  
● Code review comments will be documented  
● Teams will document problems in bug tracker

## Design Documents 
### Agile Development 
● Requirement description  
● Breakdown project into Epics  
	– Each epic is a major function  
	– e.g. application front and back ends  
● Each epic can be broken into User Stories  
	– Each story describes an individual piece of work  
	– e.g. metrics collection, database connectivity, interface design  
	- "I as a user want to view process metrics for a given process running on a Windows computer."
● Every story can be broken into tasks  
	– e.g. scraping /proc for metrics, calling JNI for length of a clock tick  
	– User Stories should list dependencies on other stories (pre-requisites and  
	co-requisites)  
● Consider how each story will be tested

**Structure**
● Introduction  
	– Authors  
● Who prepared this document?  
	– Document revision history  
● Major changes, with dates & times  
	– Audience  
● Who is this document for?  
● Who will be reading it, and what will they do with it?  
	– Developers, testers, documentation writers  
	– Table of Contents  
● Usually auto-generated from section headers  
● Let your word processor do the work for you!

**Objective and Approach**
Explains the WHY?
- Make a good argument for what you're trying to accomplish. We are trying to sell someone on this. 
● Objective  
	– What is the problem?  
● Approach  
	– How are we going to solve it?  
	– Very broad, overall design  
	– A block diagram here can be helpful as an  
	illustration

**External Design**
● How will this look from the outside world?  
● What will the interfaces be?  
	– GUI and/or CLI  
		● Can show GUI mockups  
		● Can show CLI examples and arguments  
	– API  
		● Enumerate methods / function calls  
		● Document assumptions and requirements for each  
● Use cases  
	– User actions  
	– System events  
		● Startup / shutdown / database pruning

**Internal Design**
● Development Standards  
	– Waterfall? Agile?  
	– What languages will we use?  
	– Code reuse  
● Libraries  
	– Software license?  
		● Proprietary  
		● Free/Open Source
● Hardware Resources  
- Do we need resources on the cloud? What OS is it going to run on?
	– Physical machines  
	– Operating systems  
	– Application software  
● Development environment  
	– Compilers  
	– IDE (Cursor for new AI copilot work)
	– Source code repository  
	– Defect tracker  
	– Build process  
	– Release process

**Software Flow**
● Initialization  
● Metrics collection  
● Data aggregation  
● Database storage  
● UI data extraction  
● Metrics presentation to user  
● Termination
● Error handling and recovery  
	– What do the various components do in an error?  
		● Log it? Fail noisily? Crash? Swallow the error?  
● Testability  
	– Test environment  
	– Test scenarios  
	– Regression testing  
	– Function test  
	– System test

**Packaging**
● How will the software be packaged?  
● How will it be installed?  
● How will the customer get the software?  
● Performance objectives

**Security**
● Required authority  
	– Does the software need to run as  
	root/admin?  
	– What permissions should the installed files  
	have?  
	– Who should be permitted to interface with  
	the software?  
		● Admin / user roles?
