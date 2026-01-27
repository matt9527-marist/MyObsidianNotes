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