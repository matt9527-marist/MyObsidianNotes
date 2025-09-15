Example project:
- book.h
- book.cpp
- main.cpp

```c++
// book.h  
#ifndef BOOK_H  
#define BOOK_H  
#include <string>  
class Book {  
	private:  
	std::string title;  
	std::string author;  
	int id;  
	int pages_read{0};  
	public:  
	// constructor:  
	Book(std::string t, std::string a, int i);  
	void PrintBookData();  
	void IncrementPagesRead();  
};  
#endif
```

```c++
// book.cpp  
#include <iostream>  
#include <format>  
#include "book.h"  
//initializer list  
//Mandatory for initializing const members and references  
Book::Book(std::string t, std::string a, int i)  
	: title{t}, author{a}, id{i} {}  

void Book::PrintBookData() {  
	std::cout << std::format("Book ID {}: {} by {}; Pages read {}\n",  
	id, title, author, pages_read);  
}  

void Book::IncrementPagesRead(){  
	this->pages_read++;  
}
```

```c++
// main.cpp
#include <iostream>
#include <string>
#include "book.h"
int main() {
	//Brace Initialization (Direct initialization)
	Book book_1{"C++", "Author 1", 101};
	Book book_2{"Mastering C++", "Author 2", 102};
	Book book_3{"Modern C++", "Author 3", 103};
	
	book_1.IncrementPagesRead();
	book_2.IncrementPagesRead();
	
	book_1.PrintBookData();
	book_2.PrintBookData();
	book_3.PrintBookData();
}
// g++ -std=c++23 main.cpp book.cpp && ./a.out
/*  
Book ID 101: C++ by Author 1; Pages read 1  
Book ID 102: Mastering C++ by Author 2; Pages read 1  
Book ID 103: Modern C++ by Author 3; Pages read 0  
*/
```

**How to Scale Up**
```c++
// main.cpp
#include "book.h"
int main() {
	Book book_1{"C++", "Author 1", 101};
	Book book_2{"Mastering C++", "Author 2", 102};
	Book book_3{"Modern C++", "Author 3", 103};
	Book book_99{"Book 99", "Author 99", 199};
	Book book_100{"Book 100", "Author 100", 200};
}
```
Suppose we do not just want to create 3-5 objects, but instead hundreds of objects. 
Instead of creating 100 objects, we create a vector of pointers. 
	• std::vector<Book*> book_vect;  
	• Next, we must create 100 objects and store their addresses in this  
	vector.  
	• We can use new to create a memory on the heap for the objects and  
	push back that memory to the vector. (new must have delete to  
	avoid memory leak)
```
Book *bp{nullptr}; // nullptr  
In Loop: bp = new Book{title, author, 101+I};  
book_vect.push_back(bp);
```
• Processing member methods using -> operator on the pointer  
or dereference using * and then .notation  
```
for(Book* bp : book_vect){  
	bp->IncrementPagesRead();  
	(*bp).IncrementPagesRead();  
}  
```
• After processing  
```
for(auto bp : book_vect) // auto or Book*  
	delete bp;  
book_vect.clear();
```
When we are using `new`, it allocates the memory on the heap. When we are allocating memory, we need to at some point relieve/delete the memory. We must use `delete` in order to avoid a memory leakage- when memory is allocated but is not in use. 

**Benefits of OOP in C++**
• Efficiency and Scalability: Easily generating 100 books with different authors and simplifying  
the operations  
• Code Organization:  
	• Classes to manage attributes and behaviors.  
	• Reduces complexity compared to manually creating multiple variables.  
• Pointers and Memory Management:  
• new keyword allocates memory on the heap for objects.  
• -> operator dereferences pointers and accesses object attributes/methods.  
• delete will deallocate the memory.  
• Memory allocated using new (on heap) must be deallocated using delete to avoid memory  
leak.



