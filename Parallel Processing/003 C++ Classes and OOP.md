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

