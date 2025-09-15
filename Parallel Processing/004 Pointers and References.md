A **reference** is another name given to an existing variable.
The *&* operator can be used to declare a reference on the left-hand side of any variable declaration. 

```C++
#include <cassert>  
int main(){  
	int i{5};  
	int& ref_i{i};  
	
	assert(i == ref_i);  
	assert(&i == &ref_i);  
}
```
`ref_i` will refer to `i` as an alias. We can access the value of `i` either by referencing `i` itself or by using its reference variable. 

**Pointers vs. References**
- **Pointer**: A variable that stores the memory address of another variable.  
    Syntax: `int* ptr = &var;`
    - Can be null
    - Can be reassigned
    - Needs explicit dereferencing
- **Reference**: An alias for an existing variable.  
    Syntax: `int& ref = var;`
	- Cannot be null 
	- Cannot be reassigned after initialization
	- Automatically dereferenced
## Pointers

A variable that stores the memory address
- Operating on a pointer to an object may be more efficient than the same operation on the object itself. 
- If the pointer points to a large object, passing the pointer to a function can be much more efficient than passing a copy of the object as with pass-by-value. 

```C++
#include <cassert>  
	int main(){  
	
	int i{5};  
	int* ptr_i{&i};  
	
	assert(&i == ptr_i);  
	assert(i == *ptr_i);  
}
```

Example of Pointer Usage vs. Reference Usage:
```C++
#include <cassert>  
	int main() {  
	int i{5};  
	
	int& ref_i{i}; // reference, another name & on LHS  
	int* ptr_i{&i}; // mem add & RHS  
	
	assert(i == ref_i); // ref_i is another name of i  
	assert(i == *ptr_i); // * dereference on RHS  
	
	assert(&i == &ref_i); assert(&i == ptr_i); // hexadecimal  
	
	i++;  
	assert(i == ref_i); assert(i == *ptr_i);  
	assert(&i == &ref_i); assert(&i == ptr_i);  
}
```

![[Pasted image 20250915192549.png]]
**Step by step:**
1. `int i{5};`  
    Initializes `i` to `5`.
2. `int& j{i};`  
    Declares `j` as a reference to `i`. That means `j` is just another name for `i`.
3. `int *k{&i};`  
    Declares `k` as a pointer to `i`. So `k` stores the address of `i`.  
    (Note: `k` is not used in the output.)
4. `std::cout << j << "\n";`  
    Prints the value of `j`. Since `j` is a reference to `i`, this is equivalent to printing `i`.

Printing `k` as opposed to `j` will print the address of `i` as it is a pointer. 

Example:
```c++
#include <cassert>  
int main() {  
	int i{5};  
	int& ref_i{i}; // reference, another name & on LHS  
	int* ptr_i{&i}; // mem add & RHS  
	assert(i == ref_i); // ref_i is another name of i  
	assert(i == *ptr_i); // * dereference on RHS  
	assert(&i == &ref_i); assert(&i == ptr_i); // hexadecimal  
	i++;  
	assert(i == ref_i); assert(i == *ptr_i);  
	assert(&i == &ref_i); assert(&i == ptr_i);  
}
```

**Pointers to Other Object Types**
• A pointer holds the memory address.  
• A pointer declaration must include the type of the object being  
pointed.
```c++
int i{5};  
int* ptr_i{&i};  
std::vector<int> v{1, 2, 3};  
std::vector<int> *ptr_v{&v};
```
Printer to a vector: printing elements:
```c++
#include <iostream>  
#include <vector>  
int main() {  
	std::vector<int> v{1, 2, 3};  
	std::vector<int> *ptr_v{&v};  
	
	//dereference the ptr_v to get v  
	// get the element with []  
	for(int i{0}; i < v.size(); i++)  
		std::cout << (*ptr_v)[i] << " ";  
	std::cout << "\n";  
}
```
When we have a pointer to a vector, to access the values, first we need to dereference. 
Pointer to vector: using range-based `for`
```c++
#include <iostream>  
#include <vector>  
int main() {  
	std::vector<int> v{1, 2, 3};  
	std::vector<int> *ptr_v{&v};  
	
	// dereference the ptr_v to get v  
	// use range-based for  
	for (auto elem : *ptr_v)  
		std::cout << elem << " ";  
	std::cout << "\n";  
	}
```
This is easier because we are automatically dereferencing. 

**Two Versions of a Function: Pointer vs. Reference**
```c++
#include <iostream>  
void depositMoney(double* balance, double amount) {  
	std::cout << "using pointer\n";  
	*balance += amount;  
}  
void depositMoney(double& balance, double amount) {  
	std::cout << "using reference\n";  
	balance += amount;  
}
```
In this function, balance in the first case is passed as a *pointer*, but in the second case, it is passed as a *reference*.

Pointer or reference?
```c++
void depositMoney(double& balance, double amount); //reference  
void depositMoney(double* balance, double amount); //pointer  

int main() {  
	double acc_bal{100.0};  
	double* ptr_bal = &acc_bal;  
	
	depositMoney(acc_bal, 50.0); //pointer or reference?  
	depositMoney(&acc_bal, 50.0); //pointer or reference?  
	depositMoney(ptr_bal, 50.0); //pointer or reference?  
	
	std::cout << "Balance: $" << acc_bal << "\n";  
}
/*  
using reference  
using pointer  
using pointer  
Balance: $250  
*/
```

Returning a Pointer from a Function:
```c++
#include <iostream>  
double* depositMoney(double &balance, double amount) {  
	std::cout << "using pointer\n";  
	balance += amount;  
	return &balance;  
}  

int main() {  
	double acc_bal{100.0};  
	double* ptr_acc_bal{&acc_bal};  
	
	ptr_acc_bal = depositMoney(acc_bal, 50.0);  
	
	std::cout << "Balance: $" << acc_bal << "\n";  
	std::cout << "Balance: $" << *ptr_acc_bal << "\n";  
}
/*  
using pointer (function returns a pointer)
Balance: $150  
Balance: $150  
*/
```

Dangling Pointer 
```c++
#include <iostream>  
double* depositMoney(double balance, double amount) {  
	std::cout << "using pointer\n";  
	balance += amount;  
	return &balance;  
}  

int main() {  
	double acc_bal{100.0};  
	double* ptr_acc_bal = &acc_bal; 
	 
	ptr_acc_bal = depositMoney(acc_bal, 50.0);  
	
	std::cout << "Balance: $" << acc_bal << "\n";  
	std::cout << "Balance: $" << *ptr_acc_bal << "\n";  
}
/*  
g++ -Werror -std=c++23 main.cpp  
main.cpp:5:11: error: address of stack memory associated  
with parameter 'balance' returned [-Werror,-Wreturn-stack-  
address]  
5 | return &balance;  
| ^~~~~~~  
1 error generated.  
*/
```

**Safer Alternative Using Dynamic Memory**  
• Instead of returning a pointer to the local variable, we can  
allocate memory on the heap using `new`.  
• We can return this memory address, which remains valid until  
explicitly deallocated, using `delete`.  
• The pointer will remain valid even outside the scope of the  
function.

Safe Pointer Returned from Function:
```c++
#include <iostream>  
double* depositMoney(double balance, double amount) {  
	double* ptr = new double; // allocate the memory first
	*ptr = balance; //*ptr=&balance will not work as it overwrites  
	*ptr += amount;  
	return ptr;  
}  

int main() {  
	double acc_bal{100.0};  
	double* ptr_acc_bal{nullptr};
	  
	ptr_acc_bal = depositMoney(acc_bal, 50.0);  
	
	std::cout << "Balance: $" << *ptr_acc_bal << "\n"; // safe  
	delete ptr_acc_bal;  
}
```