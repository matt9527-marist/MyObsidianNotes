How can we store metrics? 
● How can we store the metrics we collect?  
● With a database, of course!  
● It's a great way to put away information that  
we'll need later, and can easily be accessed  
for reporting purposes

● In the interests of simplicity, we can start with  
*SQLite*  
● It's an embedded database that fits right into  
our code  
	– No need to bother with database servers,  
	administration, processes, etc.  
	– It Just Works  
	– It has bindings for many different programming  
	languages

**Metrics Recording**
● Project code needs some kind of update  
mechanism  
● Read metrics from appropriate sources  
during an interval  
	– 15 seconds?  
● Store metrics in a timestamped row in the  
database  
	– Can use Java System.nanotime() here

**Metrics Aggregation**
● Data for some sources can be stored as cumulative  
values  
	– Number of seconds of CPU time  
	– Number of page faults  
● Can create a delta value to determine consumption over  
a given interval  
● Can create a CPU using %  
	– Sum all the CPU times over an interval,  
	– Dividing the interval time multiplied by the number of CPUs

