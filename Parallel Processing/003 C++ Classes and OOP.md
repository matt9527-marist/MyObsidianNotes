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

