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
