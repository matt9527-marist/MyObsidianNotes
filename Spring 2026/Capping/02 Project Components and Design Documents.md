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