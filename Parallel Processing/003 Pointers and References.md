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

## Pointers

A variable that stores the memory address
- Operating on a pointer to an object may be