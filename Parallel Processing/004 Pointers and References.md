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

Example of Pointer Usage:
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

