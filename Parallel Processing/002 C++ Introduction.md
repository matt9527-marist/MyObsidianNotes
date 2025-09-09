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
[[fallthrough]];
```
in the place of *break* statements if we do not want to add the flag. 

(or just use *break*, as is usual practice)

**Accessing a Resource**
Another good practice that we want to use is simulating access rights. 
```c++
#include <iostream>  
int getResource() {  
	srand(time(0));  
	// simulate access rights  
	return rand() % 2; // 0 ≤ rand() ≤ RAND_MAX  
}
```
Suppose we want to set a permission for obtaining a resource. This function is simply returning the number 0 or 1. *srand* ensures that the program will give a different output each time. Mod 2 ensures the output is 0 or 1. 
Using this function...

**If Statements**
```c++
int main() {  
	int access{getResource()}; //Notice brace initialization
	if(access){  
		std::cout << "Access granted\n"; //if non-zero  
	}else{  
		std::cout << "Access not granted\n"; //if zero  
	}  
	std::cout << access << "\n";  
}  
/*  
Access granted  
1  
*/
```
This program makes a request to getResource(), granting or not granting it, as per 0 or 1. 

If statement with Initializer:
```c++
#include <iostream>  
int getResource() {  
	srand(time(0));  
	return rand() % 2;  
}  
int main() {  
	if(int access{getResource()}; std::cout << access, access){  
		std::cout << "Access granted\n"; //if non-zero  
	}else{  
		std::cout << "Access not granted\n"; //if zero  
	}  
}  
//1Access granted
```

Switch statement with Initializer:
```c++
int main() {  
	switch(int access{getResource()}; access){  
	case 1:  
		std::cout << "Access granted\n"; //if non-zero  
		break;  
	case 0:  
		std::cout << "Access not granted\n"; //if zero  
	}  
}  
//Access granted
```

Using *Yoda Condition*
```c++
#include <iostream>  
int main(){  
	int access{0};  
	if(1==access)  
		std::cout << "Access\n";  
	else  
		std::cout << "No Access\n";  
}  
//No Access
```

Custom data type: *Enumerator*
Enumerator data types are user-defined. 
- Unscoped enum: not recommended
- Scoped enum using class: recommended 

Unscoped Enum:
```c++
#include <iostream>  
int main() {  
	enum Status {won, lost, keepRolling}; // 0 1 2  
	Status gameStatus{keepRolling};  
	std::cout << gameStatus << "\n"; // 2  
	
	if(2 == gameStatus)  
		std::cout << "continue game\n";  
	else  
		std::cout << "terminate\n";  
	if(gameStatus == keepRolling)  
		std::cout << "continue game\n";  
	else  
		std::cout << "terminate\n";  
}
```
When it is unscoped, our C++ environment will assign values of 0, 1, 2. This automated conversion is used.

Scoped Enum:
```c++
#include <iostream>  
int main() {  
	enum class Status {won, lost, keepRolling};// 0 1 2  
	Status gameStatus{Status::keepRolling};  
	
	//std::cout << gameStatus << "\n"; // error  
	std::cout << static_cast<int>(gameStatus) << "\n"; // 2  
	
	if(2 == static_cast<int>(Status::keepRolling))  
		std::cout << "continue game\n";  
	if(gameStatus == Status::keepRolling)  
		std::cout << "continue game\n";  
}
```
Here, we are adding *class* to the statement. The system however will not be assigning this automatic conversion to the variables!

Scoped Enum class (start with 1):
```c++
#include <iostream>  
int main() {  
	enum class Month {January=1, February, March, April, May, June, July,  
	August, September, October, November, December}; 
	 
	if (1 == static_cast<int>(Month::January))  
		std::cout << "It's January\n";  
	else  
		std::cout << "It's not January\n"; //p  
}  
//It's January
```

Using Enum declaration:
```c++
#include <iostream>  
enum class Month {January=1, February, March, April, May, June, July,  
August, September, October, November, December};  
using Month::January;  

int main() {  
	if (1 == static_cast<int>(January))  
		std::cout << "It's January\n";  
	else  
		std::cout << "It's not January\n"; //p  
}  
//It's January
```
