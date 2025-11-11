**What is OpenMP?**
• OpenMP is a widely supported open standard for writing parallel  
programs that use threads to share memory.  
• It works in C++ by using pragmas to instruct the compiler to utilize  
multiple threads.  

**OpenMP Variables: Shared vs. Private**
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
for (int i = 0; i < N; i++)  
array[i] = 0; // <== First touch happens here  
7