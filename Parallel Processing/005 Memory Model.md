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
	someFunction(i); // stack grows (recall from recursion)
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

Stack Limit:
174312 stack bottom: 0x16b25f33c current: 0x16aa64794
```c++
#include <iostream>  
int main() {  
	uint64_t hex1{0x16b25f33c};  
	uint64_t hex2{0x16aa64794};  
	uint64_t bytes{hex1 - hex2};  
	double mbs{bytes/(1024.0*1024.0)};  
	std::cout << "Size: " << bytes << " Bytes" << "\n";  
	std::cout << "Size: " << mbs << " MBs" << "\n";  
}  
//Size: 8367016 Bytes  
//Size: 7.97941 MBs  
```
We can also get stack memory using `ulimit -s`

**Heap Memory or Dynamic Memory**
![[Pasted image 20250915202218.png]]
**Properties of Heap Memory**
• P1: Memory is not deleted when the scope is left. The function  
can return the address, and the caller can use it.  
• P2: Variables are allocated at run-time, so size can be tailored  
based on the size required by variables.  
• P3: Memory leaks can occur if we forget to deallocate. With a 64-  
bit OS and large RAM/SSD, we have large memory available.  
• P4: Heap is shared among *threads*, we need to handle  
concurrency  
• P5: Heap memory can be fragmented

**Stack vs. Heap**
• When you call a function, it increases the stack with a stack  
frame that represents the function. When returned, the stack  
shrinks.  
• If we want data that lives from one function to another, we  
cannot use stack and need somewhere else - Heap. - get with  
`malloc` and `new`  
• Delete yourself  
• Destructor, Scope, and RAII come in to help delete consistently.  
• Modern C++ has provided handles that allocate heap and  
deallocate consistently, similar to stack.

`malloc` and `calloc`
• **malloc**: memory allocation  
	• dynamically allocate a single large block of memory with the  
	specified size.  
• **calloc**: cleared memory allocation  
	• dynamically allocate the specified number of blocks of memory of  
	the specified type. It initializes each block with a default value '0'.  
	• Both functions return a pointer of type void which can be cast into  
	a pointer of any form. If the space for the allocation is insufficient,  
	a NULL pointer is returned.

`malloc`, `calloc`, and `free`
```c++
int *p1 = (int*)malloc(sizeof(int));  

MyClass *p1 = (MyClass*)malloc(sizeof(MyClass));  

int *p1 = (int*)malloc(3*sizeof(int));  

int *p1 = (int*)calloc(3, sizeof(int));  

p1 = (int*)realloc(p1, 10 * sizeof(int));  

free(p1);
```

`malloc` (void pointer)
```c++
#include <iostream>  
#include <cstdlib>  
int main() {  
	void *p1 = malloc(sizeof(int)); // sizeof(MyClass)  
	std::cout << "Address: " << p1 << "\n"; 
	 
	free(p1);  
}  
//Address: 0x156605ee0
```
```c++
#include <iostream>  
#include <cstdlib>  
int main() {  
	void *p1 = malloc(sizeof(int)); // sizeof(MyClass)  
	std::cout << "Address: " << p1 << "\n";  
	
	std::cout << "Value: " << *p1 << "\n"; //error  
	// Error since size not available whether int/double  
	// casting required  
	
	free(p1);  
}
/*  
main.cpp:8:29: error: ISO C++ does not allow indirection on  
operand of type 'void *' [-Wvoid-ptr-dereference]  
8 | std::cout << "Value: " << *p1 << "\n";  
| ^~~  
main.cpp:8:26: error: invalid operands to binary expression  
('basic_ostream<char, char_traits<char>>' and 'void')  
8 | std::cout << "Value: " << *p1 << "\n";  
*/
```

`malloc` (Cast the pointer)
```c++
#include <iostream>  
#include <cstdlib>  
int main() {  
	int *p2 = (int*)malloc(sizeof(int));  
	if (p2 != nullptr) {  
		std::cout << "Address: " << p2 << "\n";  
		std::cout << "Value: " << *p2 << "\n";  
	}  
free(p2);  
}  
//Address: 0x145605ee0  
//Value: 0
```

Memory for 3 `int`s using `malloc`
```c++
#include <iostream>  
#include <cstdlib>  
int main() {  
	int *p1 = (int*)malloc(3*sizeof(int));  
	p1[0] = p1[1] = p1[2] = 5;  
	
	std::cout << p1[0] << " " << *p1 << "\n";  
	std::cout << p1[1] << " " << *(p1+1) << "\n";  
	std::cout << p1[2] << " " << *(p1+2) << "\n"; 
	 
	free(p1);  
}  
//5 5  
//5 5  
//5 5
```
using `calloc`
```c++
#include <iostream>  
#include <cstdlib>  
int main() {  
	int *p1 = (int*)calloc(3, sizeof(int));  
	p1[0] = p1[1] = p1[2] = 5;  
	
	std::cout << p1[0] << " " << *p1 << "\n"; // 5 5  
	std::cout << p1[1] << " " << *(p1+1) << "\n"; // 5 5  
	std::cout << p1[2] << " " << *(p1+2) << "\n"; // 5 5  
	
	free(p1);  
}
```

## Memory Model `new`/`delete`
`new` and `delete`:
• The malloc and free are part of the C++ standard also.  
• The `new`/`delete` represents *object-oriented counterparts* to  
memory management of malloc/free.  
• In OOP, the constructor is called to initialize the variables and  
destructor free all resources.  
• We can allocate memory to an object using malloc, but then the  
constructor is not called.  
• The `new` *allocates memory and calls the constructor*.

`MyClass *myClassN = new MyClass(); delete myClassN;`

MyClass has member: `num`
```c++
#include <cstdlib>  
#include <iostream>  
class MyClass{  
	private:  
		int *num;  
	public:  
		MyClass();  
		~MyClass();  
		void setNum(int n);  
		int getNum() const;  
};

// memory allocated to num (resource)  
MyClass::MyClass(){  
	num = (int*)malloc(sizeof(int));  
}  
// num memory (resource) de-allocated  
MyClass::~MyClass(){  
	free(num);  
}

// initializer list is only for constructor  
void MyClass::setNum(int n) {  
	*num = n;  
}  
int MyClass::getNum() const{  
	return *num;  
}
```

![[Pasted image 20250915205527.png]]
This program using the above class will throw an error:
```c++
int main(){  
	MyClass *myClassM;  
	myClassM = (MyClass *)malloc(sizeof (MyClass));  
	myClassM->setNum(5);  
	free(myClassM) ;  
}
```
Here, you are using `malloc` to allocate raw memory for `MyClass`.  
Problem: `malloc` only allocates memory but does **not call the constructor** of `MyClass`.
Because the constructor is never called, the member pointer `num` is left **uninitialized**. Later when you call:
`m1->setNum(5);`
it tries to dereference an uninitialized pointer (`num`), leading to **undefined behavior** (likely a segmentation fault).

Instead:
```c++
int main(){  
	MyClass *m1 = (MyClass *)malloc(sizeof (MyClass));  
	//m1->setNum(5); // num is not allocated  
	free(m1);  
	// num is not de-allocated  
}
```
Or we can use `new`:
```c++
nt main(){  
	//MyClass *m1 = (MyClass *)malloc(sizeof (MyClass));  
	MyClass *m1 = new MyClass();  
	
	m1->setNum(5); // num is allocated  
	
	//free(m1);  
	delete m1;  
	
	// num is de-allocated  
	std::cout << "complete\n";  
	}  
	//complete
```

**Differences between malloc/free and new/delete**
Unlike `malloc` and `free`, `new` and `delete` call the constructor/destructor
![[Pasted image 20250915205757.png]]
• *Operator Overloading*: As malloc and free are functions defined in a library,  
their behavior can not be changed easily. However, the new and delete  
operators can be overloaded by a class to include optional proprietary  
behavior.

