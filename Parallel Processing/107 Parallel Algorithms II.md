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
• Parallel sums ≠ serial sums due to non-associativity  
• Finite-precision arithmetic:  
	• Reordering in parallel -> different results  
	• Larger arrays worsen the inaccuracy  
• Catastrophic cancellation:  
	• Subtracting nearly equal values -> loss of precision

• Example:  
• Subtracting 1.0000001−1.0000000 may yield few significant digits +  
noise  
• Solution Direction:  
• Use algorithms that preserve order or improve reproducibility of results

**Catastrophic Cancellation**
• What is Catastrophic Cancellation?  
	• Occurs when subtracting two nearly equal numbers  
	• Significant digits cancel out, leaving few accurate digits  
	• Remaining digits are often just rounding noise  
• Why It Matters:  
	• Leads to large relative error, even if absolute error is small  
	• Common in parallel computing, scientific calculations, and poorly designed  
	algorithms

```c++
#include <iostream>  
int main() {  
	int x = 12.15692174374373 - 12.15692174374372;  
	std::cout<< x <<"\n";  
}
```
![[Pasted image 20251103195207.png]]
Instead of showing us 0.000000000000000001, but other digits are visible. 

**Precision Loss in Parallel Global Sum**
• Example result: only a few significant digits remain  
• Extra digits = noise from finite-precision errors  
• Parallel sum changes the addition order:  
	• Each processor sums a portion -> then combines  
• Order change -> different result from the serial sum  
• Affects reproducibility and accuracy  
• Root Cause:  
	• Reduction pattern in parallel sums  
	• Enhanced by vectorization, threads, and modern hardware  
• Key Concern:  
	• Is the parallelization mathematically sound if results change?

**Reduction & the Global Sum Issue**
• A reduction operation reduces an array to fewer dimensions, often to a scalar.  
• Common in Parallel Computing:  
	• Example: total mass or energy -> sum of global array  
	• Reduction affects both performance and correctness  
• Global Sum Issue:  
	• Serial result: always the same, but slightly inexact  
	• Parallel result: often more accurate, but not identical to serial  
	• Caused by different addition order in parallel

**Reduction & the Global Sum Issue**
• Hidden Errors:  
	• Differences are not always due to arithmetic  
	• Often from parallel bugs, e.g., outdated ghost cells not synced between  
processors  
• Takeaway:  
	• Always verify correctness — inexact ≠ incorrect, but inconsistency may  
	signal a bug

**Leblanc Problem Overview**
• High-pressure & low-pressure regions separated by a diaphragm  
• Strong shock -> large dynamic range in variables  
• Energy values:  
	• High:  1.0 × 10 −1  
	• Low:  1.0 × 10 −10
	• Dynamic range: 9 orders of magnitude  
• Numerical Challenge:  
	• Double-precision -> ~16 significant digits  
	• Adding low to high -> ~7 useful digits remain  
• Order of addition matters:  
	• High -> Low: small values contribute little  
	• Low -> High: small values add up accurately first  

**Illustration**
• Problem size: 134,217,728 values  
	• Half high, half low  
	• Summing low first improves accuracy  
• Possible Solution:  
	• Sort values: smallest -> largest before summing -> More accurate result  
• Note:  
	• Other techniques exist that are more efficient than sorting

## Techniques for Accurate Global Summation
**Long Double Summation**  
• Uses long double (80-bit on x86) as accumulator  
• Easy to implement, but not portable  
• Slight improvement in accuracy
```c++
double do_ldsum(const double* var, std::size_t ncells) {  
long double ldsum = 0.0L;  
for (int i = 0; i < ncells; ++i) {  
	// cast to long double for precision  
	ldsum += static_cast<long double>(var[i]); 
	}  
return static_cast<double>(ldsum); // return as double  
}
```

**Pairwise Summation**  
• Pairwise Summation  
• Recursively adds adjacent pairs  
• Needs extra memory  
• Accurate but slower with multiple steps

```c++
#include <vector>  
#include <cmath>  
double do_pair_sum(const double* var, int ncells) {  
	if (ncells % 2 != 0 || ncells == 0) {  
		throw std::invalid_argument("Array size must be a non-zero even number.");  
	}  
	std::vector<double> pwsum(ncells / 2);  
	Int nmax = ncells / 2;  
// Initial pairwise summation  
	for (int i = 0; i < nmax; i++) {  
		pwsum[i] = var[i * 2] + var[i * 2 + 1];  
	}  
// Recursive pairwise reduction  
	while (nmax > 1) {  
		for (int i = 0; i < nmax / 2; ++i) {  
			pwsum[i] = pwsum[i * 2] + pwsum[i * 2 + 1];  
		}  
		nmax /= 2;  
	}  
	return pwsum[0];  
}
```

**Kahan Summation**  
• Tracks small errors with a correction variable  
• Practical, low-cost on modern CPUs  
• Good for running summation

```c++
double do_kahan_sum(const double* var, int ncells) {  
	struct ErrorSum {  
		double sum = 0.0;  
		double correction = 0.0; // Tracks small error terms  
	};  
	ErrorSum local;  
	for (int i = 0; i < ncells; ++i) {  
	double corrected_next_term = var[i] + local.correction;  
	double new_sum = local.sum + corrected_next_term;  
	// Compensation  
	local.correction = corrected_next_term - (new_sum - local.sum); 
	local.sum = new_sum;  
	}  
	return local.sum;  
}
```

**Knuth Summation**  
• More general than Kahan (either value may be larger)  
• Tracks and combines multiple errors  
• Slightly higher cost (~7 FLOPs)

```c++
#include <iostream>  
#include <cstddef> // for std::size_t  
int main()  
	{  
	double do_knuth_sum(const double* var, std::size_t ncells) {  
	struct ErrorSum {  
		double sum = 0.0;  
		double correction = 0.0;  
	};  
	ErrorSum local;  
	for (int i = 0; i < ncells; ++i) {  
		double u = local.sum;  
		double v = var[i] + local.correction;  
		double upt = u + v;  
		double up = upt - v;  
		double vpp = upt - up;  
		local.sum = upt;  
		local.correction = (u - up) + (v - vpp); // Capture remaining error  
	}  
	return local.sum + local.correction;  
	}  
}
```