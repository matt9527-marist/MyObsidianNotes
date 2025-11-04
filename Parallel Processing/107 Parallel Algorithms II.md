Until now we have completed problems in the domain of hashing. 

## Prefix Sum (Scan) pattern and its importance in parallel computing 
**Types and Implementation of Prefix Scan**
• Exclusive scan: sum excludes current element  
• Inclusive scan: sum includes current element
![[Pasted image 20251103192355.png]]

**Step-efficient Parallel Scan**
• Minimizes steps, not total operations  
• Uses tree-based reduction (see Fig)  
• Each step: sum with element 1, 2, 4... positions before  
• All threads stay active -> efficient hardware usage  
• Produces an inclusive scan

**Performance**
![[Pasted image 20251103192538.png]]
O(log2n)
8 threads --> 8 numbers
pairwise sum 

> Key Question: Can we achieve same total work as serial with parallel speed?

**Work-Efficient Parallel Scan**
• Focuses on minimizing total operations  
• Uses two phases:  
	• Upsweep (right sweep)  
	• Downsweep (left sweep)  
• Fewer operations than a step-efficient scan  
• Reuses computations -> Total work =  O(n)
• Requires more steps than a step-efficient scan  

**Pattern Summary**
• Upsweep: fewer threads active over time  
• Downsweep: starts with one thread, ends with all active  
• Trade-off:  
	• Efficient in operations, but slower if few threads available

**Upsweep Phase of Work-Efficient Scan**
• Performed top to bottom (right sweep)  
• Fewer operations than a step-efficient scan  
• Every other value is left unmodified  
• Builds partial sums in a tree-like pattern  
• Prepares data for the downsweep phase  
• Result:  
	• Efficient aggregation with fewer total computations

**Upsweep Phase of Work-Efficient Scan** - 4 threads 
![[Pasted image 20251103192729.png]]

**Downsweep Phase of Work-Efficient Scan** - 4 threads 
• Left sweep following the upsweep  
• Begins by setting the last value to 0  
• Tree-based sweep to compute final exclusive scan  
• Reuses earlier results for efficiency  
• Total operations remain O(n)  
• Steps: O(log 2 n)  
• Pattern:  
	• Threads decrease in upsweep, increase in downsweep  
	• Ends with all threads busy  
• Limitation:  
	• Bound by the available GPU workgroup size or CPU threads  
![[Pasted image 20251103192855.png]]

**Parallel Scan for Large Arrays**
![[Pasted image 20251103192922.png]]
• Uses 3 GPU kernels for scalability  
• Kernel 1: Reduction sum per workgroup -> temp array  
• Kernel 2: Scan over temp array to get workgroup offsets  
• Kernel 3: Final scan on original array + offsets applied

![[Pasted image 20251103192939.png]]
• Reduce -> temp array  
• Scan -> offsets  
• Final scan -> adjusted results

## Parallel Global Sum & Associativity Problem




