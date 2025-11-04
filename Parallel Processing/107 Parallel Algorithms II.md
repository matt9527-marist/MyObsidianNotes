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
