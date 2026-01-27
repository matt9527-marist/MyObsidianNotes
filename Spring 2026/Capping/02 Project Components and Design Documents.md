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