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

**Applications**
• AMR & unstructured meshes: differential discretization  
• Particles/objects:  
	• Molecular dynamics  
	• Smoothed Particle Hydrodynamics (SPH) simulations  
	• Game engines & graphics

**Using perfect hashing for spatial mesh operations**
• Purpose  
	• Quickly locate neighboring cells in AMR meshes  
	• Avoid costly collision handling via perfect hashing  
	• Use Cases  
		• Scientific computing: material transfer across cells  
		• Image analysis: infer data from neighboring pixels  
• Cell based AMR Neighbor Rules (CLAMR)  
	• Only 1-level difference across adjacent cells  
	• Left/Bottom neighbor = lower cell of the adjacent pair  
	• Example: ntop[nleft[ic]] retrieves second neighbor
![[Pasted image 20251027193712.png]]

**Neighbor Finding with Spatial Perfect Hash**
• Goal: Efficiently locate neighbors in a cell-based  
AMR mesh  
	• Key Operation  
		• Move material or analyze data using info from  
		adjacent cells  
		• One level jump in refinement allowed (graded  
		mesh)
	
**Naive Search for Neighbor Finding**
```c++
for (int ic = 0; ic < N; ic++) {  
	for (int jc = 0; jc < N; jc++) {  
		if (is_adjacent(ic, jc)) {  
		neighbors[ic] = jc;  
		break;  
		}  
	}  
}
```
• Concept  
	• Check every other cell to find adjacent neighbors  
	• Use (i, j, level) values to match locations

• Complexity  
	• O(N^2) time -> slow for large N  
	• Each of N cells checks N others  
• Limitations  
	• Works fine for small datasets  
	• Scales poorly for large AMR meshes  
	• Ignores spatial locality -> inefficient memory use  

**Simplified k-d Tree for Selected AMR Cells**
![[Pasted image 20251027194735.png]]
• What is a k-d Tree?  
	• k = number of dimensions (e.g., k = 2 for 2D space)  
	• A k-dimensional binary search tree for organizing points in space  
	• Alternates splits across k axes (e.g., x, then y, then x...)
![[Pasted image 20251027194800.png]]
• Advantages  
	• Much faster than naive search for large N  
	• Good spatial locality -> better cache usage  
• Considerations  
	• More complex to implement  
	• Tree must be rebuilt if the mesh changes

**Quadtree for the AMR Mesh**
• A quadtree is ideal for hierarchical 2D spatial subdivisions like this mesh.  
• Start with the entire domain (root node).  
• Subdivide into 4 quadrants.  
• For each quadrant, if it contains multiple cells or finer levels, subdivide again.  
• Recursively proceed until each leaf node contains:  
	• Either a single cell  
	• Or cells of the same refinement level
![[Pasted image 20251027194835.png]]

**Spatial Perfect Hash Algorithm to perform the  
neighbor finding**
Hash Setup:  
• Allocate hash table matching resolution of finest  
cells  
• Write Phase:  
	• For each cell, store its index in all hash buckets it  
covers  
• Read Phase:  
	• For each side (left, right, top, bottom):  
		• Compute neighbor's bucket index  
		• Read from hash to get neighbor cell
![[Pasted image 20251027194915.png]]

**Method Comparison**
![[Pasted image 20251027201257.png]]

**2D neighbor calculation with various algorithms**
• Test Setup  
	• GPU: NVIDIA V100  
	• CPU: Skylake Gold 5118 @ 2.30 GHz  
	• Results reflect Best(2018) architecture  
• Scalability  
	• Parallel speedup achievable on CPUs with 24 virtual cores  
• Code Simplicity  
	• CPU implementation of spatial hash table ≈ 12 lines of code  
	• Input: 1D arrays i, j, level for each cell
![[Pasted image 20251027201352.png]]

**Hash Sort**
![[Pasted image 20251027202341.png]]

**Performance Summary**
• No comparisons (unlike quicksort)  
• Perfect hash due to spatial  
knowledge (Δmin)  
• Uses prefix sums (parallel-friendly  
technique) during read phase  
• Runs very efficiently on GPU with  
little branching or conflict
![[Pasted image 20251027202402.png]]

**Problem with Basic Perfect Hashing:**
• In an AMR mesh, some cells are very coarse (big), some are very fine  
(small).  
• A coarse cell might cover 64 hash buckets, while a fine cell covers just 1.  
• That means:  
	• More memory used  
	• Slower writes  
	• Load imbalance in parallel (some threads do more work than others)

**Key Optimizations Introduced**
• Skip interior writes:  
	• Only the edges or boundaries of a cell are used for neighbor finding.  
	• So, don’t waste time writing the whole area of the cell to the hash table.  
• Corner/midpoint writes only:  
	• Even better: only write the corners or midpoints of the cell to the hash table.  
	• Neighbor queries only need those spots.  
• Compact hash = fewer writes:  
	• Write only one value per cell into the hash table.  
	• When looking for neighbors, read multiple locations instead.  
• Use a sentinel value (like -1):  
	• Initialize all buckets to -1 to mean "empty".  
	• This lets you skip or safely check unfilled spots during neighbor search.

![[Pasted image 20251027203706.png]]
**Optimizations**
• Writing full area -> lots of buckets  
• Writing edges -> fewer buckets  
• Writing just corners or center -> minimal writes  
• Reading from all needed spots -> gets neighbors without excess writing

**Compact Hash Tables and Open Addressing**
• Perfect hashes often contain unused space (sparsity)  
• Compression ratio can be as low as 1.25× entries  
• Hash load factor = entries / table size  
• For size multiplier of 1.25 -> load factor = 0.8  
• Typical load factor used ≈ 0.333 (i.e., 3× table size)  
• Open addressing resolves collisions:  
• Entry probes next available slot if original is occupied  
• Avoids dynamic memory allocation -> ideal for GPU
![[Pasted image 20251103183453.png]]

**Probing Strategies and Performance Tradeoffs**
• Probing options for open addressing:  
	• *Linear probing*: Try next bucket in order  
	• *Quadratic probing*: Use +1, +4, +9... offsets  
	• *Double hashing*: Use second hash for jumps  
• Quadratic probing favored: better cache usage  
• On read: stored key is compared to read key  
• Optimizations affect:  
	• Read/write count per cache line  
	• Conditional logic and cache performance

![[Pasted image 20251103183558.png]]
Compact hash matches or outperforms perfect hash with > 30× sparsity  
-> Higher benefit in parallel GPU code with less thread divergence

**Hash-Based Face Neighbor Finding (Unstructured Mesh)**
**Challenge – Finding Face Connectivity in  
Unstructured Meshes**
![[Pasted image 20251103183632.png]]
Problem: Find the connectivity map for each polygon face. 
Options:
	• Brute force face search -> too slow for large meshes  
	• k-D tree is faster, but hashing is even faster  
	• Face center -> mapped to a hash bucket
**Hash-Based Face Neighbor Finding**
• Place a dot at the center of each face  
• Map each dot to a hash bucket  
• Each cell writes:  
	• To bin 1 if face is left and up from center  
	• To bin 2 if face is right and down  
• Each face checks the opposite bin:  
	• If filled -> it's a neighbor cell  
	• If empty -> it's an external face  
• Result: Fast face neighbor detection with 1 write + 1 read per face

**Constructing the Hash Table Example**
• Hash-Based Face Neighbor Finding – Setup  
• C1-C2 share a vertical face  
• C1-C3 share a horizontal face
![[Pasted image 20251103183803.png]]
![[Pasted image 20251103184016.png]]

• Each face checks the opposite bin:  
	• If filled -> it's a neighbor cell  
	• If empty -> it's an external face
• C1 checks (6,0) -> empty -> external face  
• C2 checks (8,2) => sees C4 -> neighbor  
• C1 checks (6,1) -> empty -> external face  
• C3 checks (6,2) -> empty -> external face

**Choosing Hash Table Size**
• Exact size is hard to determine  
• Choose a reasonable size based on:  
	• Number of faces  
	• Minimum face length  
• Handle collisions as they occur  
• Example:  
• If a mesh has 500 faces, choose a table size slightly larger (e.g., 701 – a prime  
number) to reduce collisions.

