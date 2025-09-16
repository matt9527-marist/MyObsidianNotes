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
Memory may be *fragmented*, in the sense that each application running on a system may be allocated in blocks, one block for each application. 

**Virtual Memory**
• Contiguous and well-ordered blocks for each program - no interference  
• possible to run programs on various computers with different memory without any  
changes in the code.  
• Separate virtual address space from physical addresses
![[Pasted image 20250915195524.png]]

![[Pasted image 20250915195539.png]]
How will the OS manage the memory if RAM is not available? Whether the memory is available or not, the OS will allocate a fixed amount of memory to each program. This is *virtual memory*, as part of a paging scheme. 

**Address Space**
• Each program has its own 32-bit address space.  
	• Addresses range from 0 to 2^32
• Address Space and Upper Limit of Program Memory:  
	• and similarly 2^32 = 4GB

![[Pasted image 20250915200117.png]]

**Use Virtual Memory on the Disk**
• A mapping is performed by OS between
virtual address space (32bit-4GB) that the
program see and the physical addresses
of RAM and disk.
• The size is not the limit since we can use
virtual memory on the disk.
	• Windows: pagefile.sys
	• Mac: /private/var/vm/

Memory Page vs. Memory Frame:
• Memory *Page*: refers to virtual memory  
	• fixed-length contiguous block described by a single entry in  
	a page table  
	• 4KB - 16 KB depends on the OS  
• Memory *Frame*: refers to physical memory  
	• smallest fixed-length contiguous block into which memory  
	pages are mapped by the OS

**Virtual Memory Management**
When a process requests memory:
- OS allocates one or more page frames to the process
- Maps the process's logical pages to the physical page frames. 
![[Pasted image 20250915200436.png]]

![[Pasted image 20250915200622.png]]

![[Pasted image 20250915201233.png]]
![[Pasted image 20250915201346.png]]
![[Pasted image 20250915201541.png]]
Memory sections refresher:
1. **Text segment** → contains compiled machine code (instructions), not variables.
2. **Data segment** → stores **global/static variables** that are explicitly initialized with a non-zero value.
3. **BSS (Block Started by Symbol)** → stores **global/static variables** that are initialized to zero (or left uninitialized).
4. **Stack** → stores local variables inside functions (`int i`, `int j` in the code).
5. **Heap** → stores dynamically allocated variables (`new`, `malloc`).

**Memory Allocation in C++**
	• Static memory allocation  
	• Dynamic memory allocation  
	• Automatic memory allocation

**Static** Memory Allocation
• Static Allocation for:  
	• Static and Global Variables  
		• in BSS (zero init) and Data (non-zero init) segment  
	• Memory *persists lifetime*  
	• the size of variables required at the compile time.

**Dynamic** Memory Allocation
• The program may request memory at run time from the OS.  
• Allocated on *Heap*  
• limited by the address space only

**Automatic** Memory Allocation 
• Automatic Allocation for:  
	• Local variables and function parameters on the Stack.  
	• It is *allocated and de-allocated automatically*  
	• the size of variables required at the compile time.

> Create a stack overflow by creating variables on the stack: 

```c++
#include <iostream>  
int id{0}; // global on BSS  

//i is a reference and does not get reallocated on the stack in each function  call.  

void someFunction(int &i){  
	int j{1}; //local: automatic on Stack  
	std::cout << id++;  
	std::cout << " stack bottom: " << &i;  
	std::cout << " current: " << &j << "\n";  
	someFunction(i); // stack grows  
}

int main(){  
	int i{0};  
	someFunction(i);  
	std::cout << "complete\n";  
}
/*  
0 stack bottom: 0x16b25f33c current: 0x16b25f314  
1 stack bottom: 0x16b25f33c current: 0x16b25f2e4  
2 stack bottom: 0x16b25f33c current: 0x16b25f2b4  
3 stack bottom: 0x16b25f33c current: 0x16b25f284  
4 stack bottom: 0x16b25f33c current: 0x16b25f254  
5 stack bottom: 0x16b25f33c current: 0x16b25f224  
...
174307 stack bottom: 0x16b25f33c current: 0x16aa64884  
174308 stack bottom: 0x16b25f33c current: 0x16aa64854  
174309 stack bottom: 0x16b25f33c current: 0x16aa64824  
174310 stack bottom: 0x16b25f33c current: 0x16aa647f4  
174311 stack bottom: 0x16b25f33c current: 0x16aa647c4  
174312 stack bottom: 0x16b25f33c current: 0x16aa64794  
zsh: segmentation fault ./a.out  
*/
```


