**Initialization of Variables**
```C++
#include <iostream>  
int main(){  
	// warning (depends on compiler) but no error  
	int n1 = 2.7;  
	std::cout << n1 << "\n"; // 2
	  
	// compile-time cast  
	int n2 = static_cast<int>(2.7);  
	std::cout << n2 << "\n"; // 2  
	
	//int n3{2.7}; // error  
	std::cout << "Hello\n";  
}
```
For what we need in parallel programming, we prefer brace initialization: 
A warning is generated for line 4. 
- 2.7 is not an int; it is floating-point. 
At line 8, we may try a compile-time cast:
- **Type Casting** is a better practice, but not the greatest.
- **Brace Initialization** is the preferred method for variable initialization in modern C++.
```
int x{5};
```
as opposed to what we may be used to usually. 

**Switch Statements**
```C++
#include <iostream>  
int main() {  
	int value{1};  
	switch (value) {  
	case 1:  
	std::cout << "Case 1 executed\n";  
	case 2:  
	std::cout << "Case 2 executed\n";  
	default:  
	std::cout << "Default case executed\n";  
	}  
}  
/*  
Case 1 executed  
Case 2 executed  
Default case executed  
*/
```
We need *break* statements in order to restrict the execution of each case block. Without it, all cases will execute.
Change the main function accordingly:
```C++
#include <iostream>  
int main() {  
	int value{1};  
	switch (value) {  
	case 1:  
	std::cout << "Case 1 executed\n";  
	break;  
	case 2:  
	std::cout << "Case 2 executed\n";  
	break;  
	default:  
	std::cout << "Default case executed\n";  
	}  
}  
//Case 1 executed
```
Unless for whatever reason we want all the cases to execute.
However, without *break* statements, C++ will throw warnings at us. If we do not want these warnings, we need to inform the compiler by adding this flag:
g++ **-Wimplicit-fallthrough** -std=c++23 main.cpp

We can also explicitly type:
```C++
[[fallthrough]]
```

