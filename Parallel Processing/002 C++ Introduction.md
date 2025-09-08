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
- 2.7 is not an int. 

```
int x = 2.7; 
```

as opposed to what we may be used to usually. 


