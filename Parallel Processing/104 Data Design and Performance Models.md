**Performance is about Data**
• Performance models — ways to predict how fast your code runs.  
• Data structure and layout — how your data is arranged in memory.  
	• Even though code seems like the heart of programming, for  
	performance, the most important part is how data is organized and  
	accessed.

**Why Data Layout Matters**
• The way you store data decides how fast your code runs.  
• This is because data movement (memory bandwidth) is now the main  
bottleneck, not computation (flops).  
• If your code is slow, it’s probably spending time waiting on data, not doing  
math.

**Data-Oriented Design (DoD)**
• Think about data usage patterns first  
• Organize data to fit those patterns  
• Prioritize:  
	• Memory bandwidth  
	• Cache efficiency  
	• Operations on data already in cache  
• Steps:  
	• Estimate performance  
	• Predict whether a code change is worth it  
	• Identify bottlenecks

**Object-Oriented Tradeoffs**
• OOP groups data + methods for code clarity  
• But: CPU doesn't work like OOP — it processes data, not abstractions  
• Performance Costs in OOP:  
• Frequent method calls = deep call stacks  
• Instruction cache misses from jumps  
• Poor data locality when working on large arrays of objects  
• Small routines may inline, complex ones do not

**Guideline**
• OOP is fine for small-scale or UI logic  
• For compute-heavy loops, prefer:  
• Procedural code  
	• Structure of Arrays (SoA) over Arrays of Structures (AoS) 
		Structure of Arrays falls under OOP. 
	• Inlining where possible to avoid jumps and stack overhead  
• DOD Focus: Organize data for cache & CPU efficiency

**Key Principles of Data-Oriented Design**
• Operate on arrays, not single items -> better loop performance  
• Use arrays of values, not arrays of structs -> better cache usage  
• Favor inlined routines, not deep call stacks  
• Avoid hidden memory allocations — control memory explicitly  
• Use contiguous array-based lists, not pointer-chained structures  
• Improves data locality and prefetching

**DoD vs. OOP**
• DOD aligns with HPC practices  
• Helps with:  
	• Shared memory programming (e.g., OpenMP)  
	• Vectorization (needs long, homogeneous arrays)  
• OOP structures hinder:  
	• Thread-local vs. shared memory distinction  
	• Efficient use of SIMD/vector instructions

**Multidimensional Arrays**
• Understand the memory layout of 2D arrays  
• Access arrays for cache efficiency
![[Pasted image 20251013185447.png]]
• Memory Layout Matters  
• C: Row-major — last index varies fastest  
• Fortran: Column-major — first index varies fastest  
• Inner loop must match memory layout for contiguous access  
• we must remember which index should be in the inner loop to leverage  
the contiguous memory in each situation

**Conventional Way of Allocating a 2D Array in C++**
```c++
double **x = malloc(jmax * sizeof(double*));  
for (int j = 0; j < jmax; j++)  
	x[j] = malloc(imax * sizeof(double));  
	
// computation...  

for (int j = 0; j < jmax; j++) free(x[j]);  
free(x);
```
• `jmax` + 1 allocations
• Allocates 1 + `jmax` blocks -> may be scattered in heap  
• Poor for cache locality, Fortran interop, file I/O, GPU transfer  
• Still widely used due to habit and teaching


