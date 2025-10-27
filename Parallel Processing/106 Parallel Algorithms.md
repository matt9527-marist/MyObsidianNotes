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
	
**Problems with Simple Hashes**
Using just the first letter of a name (e.g., 'R' for Romero) can cause:  
	• Uneven distribution – too many people under some letters  
	• More collisions – slower lookups  
• A better hash function would consider more letters or even convert the  
string into an integer representation.

*Why Use Hash Functions?*:  Computers can’t efficiently search data like a human reading a dictionary.  
	• Hashing gives us fast access – almost like jumping directly to the right page.

**Hashing Strategies: Perfect, Minimal & Compact**
• Types of Hashes  
	• Perfect Hash:  
		• At most one entry per bucket  
		• Fast lookup, may use more memory  
	• Minimal Perfect Hash:  
		• One entry per bucket, no empty buckets  
		• Space-efficient, slower to construct  
	• Compact Hash:  
		• Compresses hash table to use less memory  
		• Allows collisions, uses key checking on lookup
![[Pasted image 20251027191654.png]]

**Why this matters in Parallel Algorithms**
• Hash functions allow independent work — processors can compute and  
store without interfering.  
• This is essential in parallel sorting, searching, or data distribution, where  
we aim for O(1) time per item.

**Hash Function Design Example**
• Simple key: First letter of last name -> uneven distribution  
• Better: hash on first 4 characters  
• Consider character set range: e.g., 52 letters -> avoid waste on 256-byte  
range
## Spatial Hashing
**Spatial Hashing & Parallel AMR**
• Use Case: Krakatau Wave Simulation  
• Need higher resolution near:  
	• Wave fronts  
	• Shorelines  
• Coarser mesh used elsewhere -> improves performance
![[Pasted image 20251027192519.png]]
• Cell-based AMR: finer resolution where
needed
• Replaces structured grid with a 1D array of
cells
• Position & size stored in separate metadata
arrays

**Mesh Structure Type**
![[Pasted image 20251027192559.png]]
**Spatial Hashing**
• Used to locate cells in unstructured AMR  
• Allows fast, parallel search of nearby neighbors  
• Enables scalable spatial operations (e.g., lookups, joins)
*Key Insight*: 
• Spatial hashing supports parallelism in irregular grids  
• AMR trades simplicity for efficiency and flexibility  
• Ideal for scientific simulations with variable spatial detail

**Spatial Hashing in AMR and Particle Simulations**
• Hashing Strategy  
• Spatial hash -> maps cells/objects into grid buckets  
• Bucket size:  
	• AMR mesh: minimum cell size  
	• Particles: interaction distance

**Performance Benefit**: Query only adjacent blocks, reduces complexity O(N^2) to O(N)
Exploits spatial locality. 

