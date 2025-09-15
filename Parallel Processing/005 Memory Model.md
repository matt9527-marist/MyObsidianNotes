This discusses the case for usage of `malloc` and `free`.

## How does C++ manage memory?
`new` is used to allocate memory. 
**Physical Memory**
• Terminated programs leave gaps in memory.  
• Fragmentation can prevent allocation of large memory blocks.  
• Shared memory access risks data overwriting.  
• Sensitive data, like bank info, can be exposed to other programs.  
• Critical concern in concurrent programs using multiple threads.

![[Pasted image 20250915195249.png]]
When a program is executed via `g++`, that program is given memory in RAM to run. 

**Virtual Memory**
• Contiguous and well-ordered blocks for each program - no interference  
• possible to run programs on various computers with different memory without any  
changes in the code.  
• Separate virtual address space from physical  
addresses