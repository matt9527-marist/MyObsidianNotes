# Parallel Processing

Objective: design and implement multi-threaded and multi-processed applications. 
We will use C++, CMake and Catch2, OOP, with a focus on shared memory limitations. 
Not using all of C++, only the components and libraries relevant to parallel processing, in order to make the most efficient use of resources. 
- C++ 
- CMake and Catch 2
	- Used for providing us structure for writing and deploying applications. 
	- Makes things significantly easier. 
- Object Oriented Programming
	- Not typically for parallel processing, but libraries still use them to build upon baseline C++. The basic program structure is all C++.

Course Content:
 **Introduction to Parallel Computing**
 We will begin by writing C++ programs and then planning how to make them parallel by observing the most expensive parts of the programs and balancing how they operate together. 
1. Parallel Computing
2. Planning for Parallelization
3. Performance Limits and Profiling
4. Data design and performance models
5. Parallel algorithms and patterns.
**CPU: Parallel Workhorse**
Exploring how to write code on multi-core systems with computers that have multiple CPUs in clusters.
6. Vectorization: FLOPs for free. How can we represent commands/program executions as vectors?
7. OpenMP: Performs with multithreading
8. MPI: Parallel Backbone
**GPUs: For Acceleration**
If on your system, we have a GPU available, we have various architectures that allow us to accelerate the processes. We do profiling to check if the programs are using the available resources. 
9. GPU Architectures and Concepts
10. GPU Programming Model
11. Directive-based GPU Programming
12. GPU Languages
13. GPU Profiling and Tools 

Introductory C++ program:
```c++
#include <iostream>

int main() {
    std::cout << "Hello World\n";
}

```
When compiling our code, we want to explicitly call c++23 in the command. 

Initial greeting program to further test:
```c++
#include <iostream>  
#include <string>  
std::string CreateGreeting(const std::string userName){  
	return "Hello, " + userName + "!";  
}  
std::string GenerateWelcomeMessage(const std::string userName){  
	std::string greeting = CreateGreeting(userName);  
	greeting += " Welcome to the class!";  
	return greeting;  
}  
int main() {  
	std::string userName = "MSCS 679L”;  
	std::cout << GenerateWelcomeMessage(userName) << "\n";  
}
```
Functions must be declared in the right order they are being called, or they must be all declared as prototypes at the top of the code. 
The following code uses the prototyping method:
```C++
#include <iostream>  
#include <string>  
std::string GenerateWelcomeMessage(const std::string userName);  
std::string CreateGreeting(const std::string userName);  

std::string GenerateWelcomeMessage(const std::string userName){  
std::string greeting = CreateGreeting(userName);  
	greeting += " Welcome to the class!";  
	return greeting;  
}  
std::string CreateGreeting(const std::string userName){  
	return "Hello, " + userName + "!";  
}  
int main() {  
	std::string userName = "MSCS 679L”;  
	std::cout << GenerateWelcomeMessage(userName) << "\n";  
}
```
The second solution is better for lots of functions, but when defining several prototypes, we may miss something important. We do not want to allow this human error to cause many headaches when compiling our code. 

## Simplifying C++ Compilation
#headers
**Header Files**
These are .h files. This is one solution we can implement to have all function declarations inherited. 
• Prevent clutter by housing function declarations separate  
from .cpp definitions.  
	• .h file to include function declarations and  
	• .cpp to include function definitions.

The following will be the structure of a given C++ program:
**Greeting Project**
![[Pasted image 20250908184334.png]]
In the header file *greeting.h*:
```C++
#ifndef GREETING_H  
#define GREETING_H  

#include <string>  

std::string GenerateWelcomeMessage(const std::string userName);  
std::string CreateGreeting(const std::string userName);  

#endif
```
We have the ifndef,define statements at the top to ensure there is no redundancy in the function definitions. If the function is defined in the main code, give the information to the compiler, if not, then move on. 

```C++
#pragma once
```
This can also be included at the top of the header file to ensure that the function is declared only once. 

greeting.cpp:
```C++
#include "greeting.h"  
#include <iostream>  
std::string GenerateWelcomeMessage(const std::string userName){  
	std::string greeting = CreateGreeting(userName);  
	greeting += " Welcome to the class!";  
	return greeting;  
}  
std::string CreateGreeting(const std::string userName){  
	return "Hello, " + userName + "!";  
}
```
What does "include" mean? Tells the compiler what to include in compilation for which functions are being used. No need to do it twice.

![[Pasted image 20250908185400.png]]
We need to specify the 
