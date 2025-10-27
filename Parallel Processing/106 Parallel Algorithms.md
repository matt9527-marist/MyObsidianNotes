• Algorithm: A step-by-step method to solve a complete problem.  
	• Example: Sorting a list, multiplying matrices, or finding the shortest path.  
• **Parallel Algorithm**: An algorithm designed to run multiple steps at the same  
time on different parts of the data.  
	• This helps solve big problems faster by using multiple processors or cores.  
• Parallel Pattern: A common piece of code that shows up in lots of programs. (like the *kernel*)
	• It does part of a job, but not the whole solution by itself. Think of it like a  
	"tool" used inside a bigger algorithm.
## Algorithm Analysis for parallel computing applications 
**Comparison Sort (like Bubble Sort)**
• Each person compares their name to a neighbor and moves accordingly.  
• This process is repeated many times.  
• Problem for parallelism: People (or processors) must wait on each other.  
• On a GPU: If a group (workgroup) finishes its row, it must stop and restart to  
work with the next row -> inefficient.  
• Performance:  
	• Comparison sorts like bubble sort have a performance of O(N^2 ) in the worst  
	case, or O(NlogN)  for better algorithms like quicksort or mergesort.  

## Performance Models with Algorithmic Complexity 
**Hash Sort**
Put a sign for each starting letter of the last name (A, B, C...).  
• Each person goes directly to the sign that matches.  
• If too many people have the same starting letter (like "S"), repeat using the second letter.  
• For small groups, use any simple sort.  
	• Key Benefit: Everyone moves independently, no waiting needed.  
• Performance: Hash sort is O(N), and even better, in parallel, it's O(N/P) if you use P processors.  
• Example: With 16 processors and 100 people:

**Hash Function**
• A hash function takes a key (like a name or string) and  
converts it into a number (called a hash).  
• This number is then used to index into an array-like  
structure called a hash table to store or find a value.  
• Think of it like this:  
	• Key = “Romero” -> gets hashed into a number, e.g.,  
	59  
	• Then we use index 59 in the table to store or look up  
	data like a username