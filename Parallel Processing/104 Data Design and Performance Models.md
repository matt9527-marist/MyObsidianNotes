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

**Contiguous Block with Pointer Setup**
```c++
double **x = malloc(jmax * sizeof(double*));  
x[0] = malloc(jmax * imax * sizeof(double));  
for (int j = 1; j < jmax; j++)  
	x[j] = x[j - 1] + imax;
```
• Only 2 allocations  
• Data is contiguous in memory  
• Fast, cache-efficient, portable  
• Easy to free, use in Fortran, or transfer to GPU

**Contiguous Block**
![[Pasted image 20251013191347.png]]
• Why It Matters  
	• Contiguous layout enables:  
	• Efficient block I/O  
	• Compatibility with numerical libraries  
	• Better vectorization and threading  
	• Avoid hidden performance traps in pointer-heavy allocation

**Single Allocation (Optimized)**
```c++
double** x = malloc(jmax * sizeof(double*) + jmax * imax * sizeof(double));  
x[0] = (double*)(x + jmax);  
for (int j = 1; j < jmax; j++)  
	x[j] = x[j-1] + imax;
```
• Just 1 allocation  
• Row pointers + data in one block -> best cache performance  
• Fast, compact, easy to free

Accessing the array:
• 1D access: x[0][i] or via double* x1d = x[0]; x1d[i]  
• 2D access: x[j][i]  
• Manual index: x1d[i + imax * j] (for threading/vectorization)

## Structure of Arrays vs. Array of Structures 
**Understanding Data Layouts in C++**
• Goal: Choose data structures that align with how the CPU loads data, not  
just how you organize code.  
*• Array of Structures (AoS)*  
*• Structure of Arrays (SoA)*  
• Hybrid: Array of Structures of Arrays (AoSoA – discussed later)

**Array of Structures (AoS)**
![[Pasted image 20251013192300.png]]
• Good when all fields are used together
• Bad when only one field (e.g., just R) is used — wastes cache bandwidth
• Note: Padding for alignment may add 25% memory overhead

**Structure of Arrays (SoA)**
![[Pasted image 20251013192353.png]]
• Good for accessing one field at a time (e.g., just R)  
• Cache efficiency can drop when all fields are accessed together  
• Memory allocations are separate (not guaranteed contiguous)

**Performance Depends on Usage Pattern**
• Example 1: All components used  
	• radius[i] = sqrt(x * x + y * y + z * z); // Best with AoS  
	• All components are accessed together  
	• Good cache usage with AoS  
• Example 2: Only one component used  
	• density_gradient[i] = (density[i] - density[i-1]) / (x[i] - x[i-1]);  
	• Accesses x only -> Better with SoA  
	• AoS loads x, y, z -> 66% of cache load wasted

**SoA Example for Spatial Coordinates**
• Efficient for both:  
	• Full 3D operations (radius[i] = sqrt(...))  
	• Single-axis calculations (density_gradient[i] = ...)  
	• But as the field count increases -> Too many memory streams for the cache

![[Pasted image 20251013192845.png]]

![[Pasted image 20251020183856.png]]

**Key Takeaways**
• Think data usage first, not just code structure  
• AoS: Good for CPU-side code using all fields together  
• SoA: Better for performance-critical, vectorized, or GPU code  
• *Use contiguous memory when possible to avoid fragmented cache loads*  
• Test both layouts if unsure — performance can vary by use case and  
hardware

C++ Classes and Performance Pitfalls
```c++
class Cell {  
	double x, y, z, radius;  
public:  
	void calc_radius() {  
	radius = sqrt(x*x + y*y + z*z);  
	}  
	void big_calc();  
};  
Cell my_cells[1000];  
for (int i = 0; i < 1000; i++)  
	my_cells[i].calc_radius();
```
• Easy to read  
• But has hidden performance issues
• Instruction cache misses: Every calc_radius() or big_calc() call jumps to  
new code locations.  
• Subroutine call overhead: Stack push/pop, jump in/out = slow  
• Cache line inefficiency: Writes to radius may force cache invalidation if  
shared across threads.  
• Inlining can help — but only for simple methods like calc_radius()  
big_calc() is too complex to inline.

**How to Make It Faster**
• Use flat arrays for x, y, z, radius  
	• Calculate in a procedural loop with dereferencing once  
	• This reduces:  
		• Instruction jumps  
		• Cache reloads  
		• Repeated pointer dereferencing

**Hash Table Example** - AoS vs. SoA
```c++
struct hash_type {  
	int key;  
	int value;  
};  
hash_type hash[1000];
```
• Key and value stored together  
• Wastes cache space if only keys are scanned
```c++
struct hash_type {  
	int* key;  
	int* value;  
};  
hash_type hash;  
hash.key = new int[1000];  
hash.value = new int[1000];
```
• Only keys are loaded into cache during search  
• Much faster for lookups  
• Also better for vectorization

Physics Simulation - more AoS vs. SoA
```c++
struct phys_state {  
	double density;  
	double momentum[3];  
	double TotEnergy;  
};  
phys_state state[1000];  
double* density = new double[1000];  
double* momentum_x = new double[1000];  
double* momentum_y = new double[1000];  
double* momentum_z = new double[1000];  
double* TotEnergy = new double[1000];
```
Prefers SoA

**Summary: Performance-Friendly C++ Tips**
• Avoid per-object method calls in tight loops  
	• Flatten data into arrays (SoA) when:  
		• Only some fields are used  
		• You need vectorization  
• You’re working with large datasets  
	• Use AoS when:  
	• All fields are used together  
	• You need simple code and don’t mind some overhead

**Why use AoSoA**
• AoSoA (Array of Structures of Arrays) is a hybrid layout that balances the  
benefits of both:  
• AoS: Good when accessing all fields together  
• SoA: Good when accessing one field at a time  
• AoSoA slices the data into blocks that match the CPU’s vector size,  
improving vectorization and cache performance.

**C++ AoSoA Implementation Example**
```c++
const int V = 4; // Set vector length
struct SoA_type {
	int R[V], G[V], B[V]; // Structure of Arrays
};

int len = 1000;
SoA_type AoSoA[len / V]; // Array of Structs of Arrays

for (int j = 0; j < len / V; j++) {
	for (int i = 0; i < V; i++) {
		AoSoA[j].R[i] = 0;
		AoSoA[j].G[i] = 0;
		AoSoA[j].B[i] = 0;
	}
}
len/4 =250
```
Performance Insight:
In benchmark studies, AoSoA matched the  
better of AoS and SoA  
• Performs well across both:  
• Cache-bound CPU code  
• SIMD vectorization  
• GPU workgroup tuning  
	• V = 1 -> behaves like AoS  
	• V = len -> behaves like SoA  
	• V = 8 -> optimal on an 8-wide vector machine

Best use for AoSoA:
- Matching the hardware
	• When your data needs both field-wide and object-wide access  
	• When you want to exploit SIMD while keeping the structure  
	• When you want a portable layout that adapts to CPU, GPU, or  
	architecture

## Cache 
**Three C's of Cache Misses**
![[Pasted image 20251020184243.png]]

