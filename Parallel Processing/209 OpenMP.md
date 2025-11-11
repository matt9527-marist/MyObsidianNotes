**What is OpenMP?**
• OpenMP is a widely supported open standard for writing parallel  
programs that use threads to share memory.  
• It works in C++ by using pragmas to instruct the compiler to utilize  
multiple threads.  

**OpenMP Variables: Shared vs. Private**
Shared vs. private threads
![[Pasted image 20251110193850.png]]
• Each thread has:  
	• Its own instruction pointer  
	• Its own stack pointer  
	• Its own stack memory (local  
	variables)  
• All threads share:  
	• Heap memory  
	• Static/global memory
![[Pasted image 20251110193912.png]]

**Work Sharing (OpenMP)**
• Means splitting a task or loop across multiple threads.  
• OpenMP does this using directives like:  
	• `#pragma omp` parallel for  

**First Touch (Memory Allocation Concept)**
• Memory isn’t truly "used" until it’s written to (first touched).  
• When that first write happens, the operating system physically assigns  
memory near the CPU core (or thread) that did the writing.  
- Pragma parallel for:
```c++
for (int i = 0; i < N; i++)  
	array[i] = 0; // <== First touch happens here  
```

**NUMA Systems**
• On systems with NUMA (Non-Uniform Memory Access):  
• Different parts of memory are closer or farther from each CPU.  
• If memory is first touched in a serial loop, it may be placed far from all  
threads.  
• That results in slower memory access when threads try to read/write it.  
• Using first touch in parallel ensures memory is placed near each thread,  
reducing access time.  

**Relaxed Memory Model (OpenMP)**
• Threads may not immediately see changes made by other threads to  
shared variables.  
• Each thread may keep variables in local cache, which isn’t updated  
instantly to main memory.  
• So, threads can get out-of-date values unless told to synchronize.  

**OpenMP Directive Handling**
![[Pasted image 20251110195615.png]]
![[Pasted image 20251110195627.png]]

**7.2**
• Definition of nthreads and thread_id in the serial region.  
• All of the threads report that they are thread number 9.  
	• This is because nthreads and thread_id are shared variables.  
	• The value that is assigned at run time to these variables is the one  
	written by the last thread to execute the instruction.  
	• This is a typical race condition.  
	• It is a common issue in threaded programs of any type.  
![[Pasted image 20251110201437.png]]
```c++
int main() {  
	int nthreads, thread_id;  
	#pragma omp parallel  
	{  
		thread_id = omp_get_thread_num();  
		nthreads = omp_get_num_threads()  
		std::cout << "Goodbye slow serial world and Hello OpenMP!\n ";  
		std::cout << "I have " << nthreads << " thread(s) and my thread id is " << thread_id << '\n';  
	}  
	return 0;  
}  
```
**7.3**
• Definition of nthreads and thread_id moved into the parallel region.  
• Now we get a different thread ID for each thread.  
• The order of the printout is random, depending on the order of the writes  
from each processor,  
• And how they get flushed to the standard output device.  
```c++
int main() {  
	#pragma omp parallel  
	{  
		int thread_id = omp_get_thread_num();  
		int nthreads = omp_get_num_threads();  
		std::cout << "Goodbye slow serial world and Hello OpenMP!\n ";  
		std::cout << "I have " << nthreads << " thread(s) and my thread id is " << thread_id << '\n';  
	}  
	return 0;  
}  

```
```c++
#include <iostream>  
#include <omp.h>  
#include <format> // C++20+, used in C++23 as well  
int main() {  
	// Set number of threads (optional)  
	omp_set_num_threads(4); // Or let it auto-detect  
	// Parallel region starts here  
	#pragma omp parallel  
	{  
		int thread_id = omp_get_thread_num();  
		int total_threads = omp_get_num_threads();  
		// Thread-safe output using C++23's std::format  
		#pragma omp critical  
		std::cout << std::format("Hello MSCS 679L! from thread {} of {}\n", thread_id, total_threads);  
	}  
	return 0;  
}  
//Hello MSCS 679L! from thread 0 of 4  
//Hello MSCS 679L! from thread 2 of 4  
//Hello MSCS 679L! from thread 1 of 4  
//Hello MSCS 679L! from thread 3 of 4
```
**7.4**
• Variables defined in a parallel region are private.  
• Places output statements into an OpenMP single pragma block  
• So, only one thread writes output.  
```c++
int main() {  
	// >> Spawn threads >>  
	#pragma omp parallel  
	{  
		int nthreads = omp_get_num_threads(); // Get total number of threads  
		int thread_id = omp_get_thread_num(); // Get this thread's ID  
		// Only one thread runs this block  
		#pragma omp single  
		{  
		std::cout << "Number of threads is " << nthreads << '\n';  
		std::cout << "My thread id is " << thread_id << '\n';  
	}  
	// Implied barrier after #pragma omp single  
	}  
	// Implied barrier after #pragma omp parallel  
	return 0;  
}  
// Number of threads is 10  
// My thread id is 2  
```
**7.5**
• Adds directive to run only on main thread  
```c++
int main() {  
	#pragma omp parallel // >> Spawn threads >>  
	{  
		int nthreads = omp_get_num_threads();  
		int thread_id = omp_get_thread_num();  
		#pragma omp masked // Only thread 0 executes this block  
		{  
			std::cout << "Goodbye slow serial world and Hello OpenMP!\n";  
			std::cout << " I have " << nthreads << " thread(s), and my thread id is " <<  
			thread_id << '\n';  
		}  
	} // Implied barrier after parallel region  
	return 0;  
}  
//Goodbye slow serial world and Hello OpenMP!  
// I have 10 thread(s), and my thread id is 0  
```
**7.6**
• Moves cout statement out of parallel region  
• Pragma applies to next statement or a scoping block delimited by curly braces.  
• Replaces OpenMP masked pragma with conditional for thread zero  
```c++
#include <iostream>  
#include <omp.h>  
int main() {  
		std::cout << "Goodbye slow serial world and Hello OpenMP!\n"; //  
		#pragma omp parallel // >> Spawn threads >>  
			{  
			if (omp_get_thread_num() == 0) { //  
			std::cout << " I have " << omp_get_num_threads()  
			<< " thread(s) and my thread id is "  
			<< omp_get_thread_num() << '\n';  
			}  
		// Implied barrier after parallel region  
	}  
	return 0;  
}  
//Goodbye slow serial world and Hello OpenMP!  
// I have 10 thread(s) and my thread id is 0  
```

**Summary**
![[Pasted image 20251110200245.png]]
## Loop-Level OpenMP

**Loop-Level OpenMP for Quick Parallelization**
• Suitable for modest parallelism needs  
• Works well with low memory requirements  
• Targets loops with high computational cost  
• Quick and low-effort parallelization  
• Reduces thread race conditions using `#pragma omp parallel` for  
• Ideal first step for adding thread-level parallelism  

Memory Allocation 
![[Pasted image 20251110203218.png]]
All the array memory is first touched by the main thread during the initialization prior to the main loop.  
This can cause the memory to be located in a different memory region, where the memory access  
time is greater for some of the threads.  

Initialization using Parallel For:
• Initialization in a “parallel for” pragma so first touch gets memory in the  
proper location  
• OpenMP for pragma to distribute work for vector add loop across threads  

**Performance Overview**
![[Pasted image 20251110203304.png]]

**How Triad Helps **