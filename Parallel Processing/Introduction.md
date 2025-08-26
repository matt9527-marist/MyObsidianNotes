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
Functions must be declared in the right order they are being called, or they must be all declared 