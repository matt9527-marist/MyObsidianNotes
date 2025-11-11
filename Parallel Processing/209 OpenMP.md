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

